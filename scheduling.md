# 任務排程

- [簡介](#introduction)
- [定義排程](#defining-schedules)
    - [排程頻率設置](#schedule-frequency-options)
    - [避免任務重複](#preventing-task-overlaps)
- [任務輸出](#task-output)
- [任務掛勾](#task-hooks)

<a name="introduction"></a>
## 簡介

在過去，開發者必須為每個需要排程的任務產生 Cron 項目。然而令人頭疼的是任務排程不受版本控制，並且你需要 SSH 到你的伺服器增加 Cron 項目。Laravel 指令調度器（command scheduler）允許你清楚流暢的在 Laravel 當中定義指令排程，並且僅需要在你的伺服器上面增加一條 Cron 項目即可。
In the past, developers have generated a Cron entry for each task they need to schedule. However, this is a headache. Your task schedule is no longer in source control, and you must SSH into your server to add the Cron entries. The Laravel command scheduler allows you to fluently and expressively define your command schedule within Laravel itself, and only a single Cron entry is needed on your server.

你的排程已經被定義在 `app/Console/Kernel.php` 檔案的 `schedule` 方法中。為了方便你開始，一個簡單的範例已經包含在該方法中。你可以自由的增加工作排程到 `Schedule` 物件中。
Your task schedule is defined in the `app/Console/Kernel.php` file's `schedule` method. To help you get started, a simple example is included with the method. You are free to add as many scheduled tasks as you wish to the `Schedule` object.

### 啟動調度器

底下是唯一需要加入到伺服器的 Cron 項目：
Here is the only Cron entry you need to add to your server:

    * * * * * php /path/to/artisan schedule:run 1>> /dev/null 2>&1


該 Cron 將於每分鐘呼叫 Laravel 指令調度器，接著 Laravel 會衡量你排定的任務並執行預定的任務。
This Cron will call the Laravel command scheduler every minute. Then, Laravel evaluates your scheduled tasks and runs the tasks that are due.

<a name="defining-schedules"></a>
## 定義排程

你可以將所有排定的任務定義在 `App\Console\Kernel` 類別的 `schedule` 方法中。一開始，讓我們看一個任務的排程範例。在該範例，我們將排定一個在午夜被呼叫的閉包。該閉包將執行清除某個資料表的資料庫查詢：
You may define all of your scheduled tasks in the `schedule` method of the `App\Console\Kernel` class. To get started, let's look at an example of scheduling a task. In this example, we will schedule a `Closure` to be called every day at midnight. Within the `Closure` we will execute a database query to clear a table:

    <?php

    namespace App\Console;

    use DB;
    use Illuminate\Console\Scheduling\Schedule;
    use Illuminate\Foundation\Console\Kernel as ConsoleKernel;

    class Kernel extends ConsoleKernel
    {
        /**
         * The Artisan commands provided by your application.
         *
         * @var array
         */
        protected $commands = [
            'App\Console\Commands\Inspire',
        ];

        /**
         * Define the application's command schedule.
         *
         * @param  \Illuminate\Console\Scheduling\Schedule  $schedule
         * @return void
         */
        protected function schedule(Schedule $schedule)
        {
            $schedule->call(function () {
                DB::table('recent_users')->delete();
            })->daily();
        }
    }

除了排定 `閉包` 呼叫，你還能排定 [Artisan 命令](/docs/{{version}}/artisan) 以及作業系統指令。舉個例子，你可以使用 `command` 方法排定一個 Artisan 指令：
In addition to scheduling `Closure` calls, you may also schedule [Artisan commands](/docs/{{version}}/artisan) and operating system commands. For example, you may use the `command` method to schedule an Artisan command:

    $schedule->command('emails:send --force')->daily();

`exec` 指令可以被用於發送指令到作業系統：
The `exec` command may be used to issue a command to the operating system:

    $schedule->exec('node /home/forge/script.js')->daily();

<a name="schedule-frequency-options"></a>
### 排程頻率設置

當然，你可以針對你的任務分配多種排程計畫：
Of course, there are a variety of schedules you may assign to your task:

方法  | 描述
------------- | -------------
`->cron('* * * * *');`  |  於自訂的 Cron 排程執行該任務
`->everyMinute();`  |  於每分鐘執行該任務
`->everyFiveMinutes();`  |  於每五分鐘執行該任務
`->everyTenMinutes();`  |  於每十分鐘執行該任務
`->everyThirtyMinutes();`  |  於每三十分鐘執行該任務
`->hourly();`  |  於每小時執行該任務
`->daily();`  |  於每天午夜執行該任務
`->dailyAt('13:00');`  |  於每天 13:00 執行該任務
`->twiceDaily();`  |  於每天 1:00 及 13:00 執行該任務
`->weekly();`  |  於每週執行該任務
`->monthly();`  |  於每月執行該任務
Method  | Description
------------- | -------------
`->cron('* * * * *');`  |  Run the task on a custom Cron schedule
`->everyMinute();`  |  Run the task every minute
`->everyFiveMinutes();`  |  Run the task every five minutes
`->everyTenMinutes();`  |  Run the task every ten minutes
`->everyThirtyMinutes();`  |  Run the task every thirty minutes
`->hourly();`  |  Run the task every hour
`->daily();`  |  Run the task every day at midnight
`->dailyAt('13:00');`  |  Run the task every day at 13:00
`->twiceDaily();`  |  Run the task daily at 1:00 & 13:00
`->weekly();`  |  Run the task every week
`->monthly();`  |  Run the task every month

這些方法可以合併其他限制條件，藉以產生更精細的排程。例如在某週的某幾天執行排程。舉個例子，排定一個每週一的排程：
These methods may be combined with additional constraints to create even more finely tuned schedules that only run on certain days of the week. For example, to schedule a command to run weekly on Monday:

    $schedule->call(function () {
        // Runs once a week on Monday at 13:00...
    })->weekly()->mondays()->at('13:00');

下方列出額外的限制條件：
Below is a list of the additional schedule constraints:

方法  | 描述
------------- | -------------
`->weekdays();`  |  限制任務在工作日
`->sundays();`  |  限制任務在星期日
`->mondays();`  |  限制任務在星期一
`->tuesdays();`  |  限制任務在星期二
`->wednesdays();`  |  限制任務在星期三
`->thursdays();`  |  限制任務在星期四
`->fridays();`  |  限制任務在星期五
`->saturdays();`  |  限制任務在星期六
`->when(Closure);`  |  限制任務基於一個為真驗證
Method  | Description
------------- | -------------
`->weekdays();`  |  Limit the task to weekdays
`->sundays();`  |  Limit the task to Sunday
`->mondays();`  |  Limit the task to Monday
`->tuesdays();`  |  Limit the task to Tuesday
`->wednesdays();`  |  Limit the task to Wednesday
`->thursdays();`  |  Limit the task to Thursday
`->fridays();`  |  Limit the task to Friday
`->saturdays();`  |  Limit the task to Saturday
`->when(Closure);`  |  Limit the task based on a truth test

#### 為真驗證限制條件

`when` 方法可以被用於限制任務執行與否，基於給定一個為真驗證的執行結果。換句話說，如果給定的 `閉包` 回傳 `true`，這個任務將持續被執行只要沒有其他的限制條件。
The `when` method may be used to limit the execution of a task based on the result of a given truth test. In other words, if the given `Closure` return `true`, the task will execute as long as no other constraining conditions prevent the task from running:

    $schedule->command('emails:send')->daily()->when(function () {
        return true;
    });

<a name="preventing-task-overlaps"></a>
### 避免任務重複

預設情況，排定的任務將被執行，即便之前相同的任務主體仍未結束。為了避免這個問題，你可以使用 `withoutOverlapping` 方法：
By default, scheduled tasks will be run even if the previous instance of the task is still running. To prevent this, you may use the `withoutOverlapping` method:

    $schedule->command('emails:send')->withoutOverlapping();

在這個範例，如果非執行中，`emails:send` [Artisan 指令](/docs/{{version}}/artisan) 將於每分鐘執行。當你有些超長執行時間的任務，而不知道確切的執行時間，`withoutOverlapping` 方法將特別有幫助。
In this example, the `emails:send` [Artisan command](/docs/{{version}}/artisan) will be run every minute if it is not already running. The `withoutOverlapping` method is especially useful if you have tasks that vary drastically in their execution time, preventing you from predicting exactly how long a given task will take.

<a name="task-output"></a>
## 任務輸出

Laravel 調度器為任務排程輸出提供許多便捷的方法。首先，透過 `sendOutputTo` 你可以發送輸出到單一檔案做為事後檢查：
The Laravel scheduler provides several convenient methods for working with the output generated by scheduled tasks. First, using the `sendOutputTo` method, you may send the output to a file for later inspection:

    $schedule->command('emails:send')
             ->daily()
             ->sendOutputTo($filePath);

透過 `emailOutputTo` 方法，你可以發送輸出到你所選的電子郵件。注意，你必須先透過 `sendOutputTo` 方法輸出到一個檔案。同時，在將任務輸出發送到電子郵件之前，你需要先設定 Laravel 的 [電子郵件服務](/docs/{{version}}/mail)：
Using the `emailOutputTo` method, you may e-mail the output to an e-mail address of your choice. Note that the output must first be sent to a file using the `sendOutputTo` method. Also, before e-mailing the output of a task, you should configure Laravel's [e-mail services](/docs/{{version}}/mail):

    $schedule->command('foo')
             ->daily()
             ->sendOutputTo($filePath)
             ->emailOutputTo('foo@example.com');

> **注意：** `emailOutputTo` 與 `sendOutputTo` 方法只適用於 `command` 方法，並且不支援 `call` 方法。
> **Note:** The `emailOutputTo` and `sendOutputTo` methods are exclusive to the `command` method and are not supported for `call`.

<a name="task-hooks"></a>
## 任務掛勾

透過 `before` 與 `after` 方法，你能讓特定的代碼在任務完成之前以及之後執行：
Using the `before` and `after` methods, you may specify code to be executed before and after the scheduled task is complete:

    $schedule->command('emails:send')
             ->daily()
             ->before(function () {
                 // Task is about to start...
             })
             ->after(function () {
                 // Task is complete...
             });

#### Ping 網址

透過 `pingBefore` 與 `thenPing` 方法，調度器能自動的在一個任務完成之前或之後 ping 一個給定的網址。該方法在你排定的任務進行或完成時，能有效的通知一個外部的服務，像是 [Laravel Envoyer](https://envoyer.io)。
Using the `pingBefore` and `thenPing` methods, the scheduler can automatically ping a given URL before or after a task is complete. This method is useful for notifying an external service, such as [Laravel Envoyer](https://envoyer.io), that your scheduled task is commencing or complete:

    $schedule->command('emails:send')
             ->daily()
             ->pingBefore($url)
             ->thenPing($url);


使用 `pingBefore($url)` 或 `thenPing($url)` 功能需要 Guzzle HTTP 函式庫。你可以透過增加下列到你的 `composer.json` 檔案，將 Guzzle 加入你的專案：
Using either the `pingBefore($url)` or `thenPing($url)` feature requires the Guzzle HTTP library. You can add Guzzle to your project by adding the following line to your `composer.json` file:

    "guzzlehttp/guzzle": "~5.3|~6.0"

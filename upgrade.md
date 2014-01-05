# 升級導引

- [從 4.0 升級至 4.1](#upgrade-4.1)

<a name="upgrade-4.1"></a>
## 從 4.0 升級至 4.1

### 升級你的 Composer 相依性

升級你的應用程式至 Laravel 4.1，將 `composer.json` 裡的 `laravel/framework` 版本更改至 `4.1.*`。

### 檔案置換

將你的 `public/index.php` 置換成 [這個 repository 的乾淨版本](https://github.com/laravel/laravel/blob/master/public/index.php)。

同樣的，將你的 `artisan` 置換成 [這個 repository 的乾淨版本](https://github.com/laravel/laravel/blob/master/artisan)。

### 新增設定檔案及選項

更新你在設定檔 `app/config/app.php` 裡的 `aliases` 和 `providers` 陣列。而更新的選項值可以在[這個檔案](https://github.com/laravel/laravel/blob/master/app/config/app.php)中找到。請確定將你後來加入自定和套件所需的 providers / aliases 加回陣列中。

從 [這個 repository](https://github.com/laravel/laravel/blob/master/app/config/remote.php)增加 `app/config/remote.php` 檔案。

在你的 `app/config/session.php` 增加新的選項 `expire_on_close`。而預設值為 `false`。

在你的 `app/config/queue.php` 檔案裡新增 `failed` 設定區塊。以下為區塊的預設值：

	'failed' => array(
		'database' => 'mysql', 'table' => 'failed_jobs',
	),

**（非必要）** 在你的 `app/config/view.php` 裡，將 `pagination` 設定選項更新為 `pagination::slider-3`。

### 更新控制器（Controllers）

如果 `app/controllers/BaseController.php` 有 `use` 語句在最上面，將 `use Illuminate\Routing\Controllers\Controller;` 改為 `use Illuminate\Routing\Controller;`。

### 更新密碼提醒

密碼提醒功能已經大幅修正擁有更大的彈性。你可以執行 Artisan 指令 `php artisan auth:reminders-controller` 來檢查新的存根控制器。你也可以瀏覽 [更新文檔](/docs/security#password-reminders-and-reset) 然後相應的更新你的應用程式。

更新你的 `app/lang/en/reminders.php` 語系檔案來符合[這個新版檔案](https://github.com/laravel/laravel/blob/master/app/lang/en/reminders.php)。

### 更新環境偵測

為了安全因素，不再使用網域網址來偵測辨別應用程式的環境。因為這些直很容易被偽造欺騙，繼而讓攻擊者透過請求來達到變更環境。所以你必須改為使用機器的 hostname（在 Mac & Ubuntu 下執行 `hostname` 出來的值）

（譯按：的確原有方式有安全性考量，但對於現行 VirtualHost 大量使用下，反而這樣改會造成不便）

### 更簡單的日誌文件

Laravel 目前只會產生單一的日誌文件: `app/storage/logs/laravel.log`。然而，你還是可以透過設定你的 `app/start/global.php` 檔案來更改他的行為。

### 刪除重定向結尾的斜線

在你的 `bootstrap/start.php` 檔案中，移除呼叫 `$app->redirectIfTrailingSlash()`。這個方法已不再需要了，因為之後將會改以框架內的 `.htaccess` 來處理。

然後，用[新版](https://github.com/laravel/laravel/blob/master/public/.htaccess)替換掉你 Apache 中的 `.htaccess` 檔案，來處理結尾的斜線問題。

### 取得目前路由

取得目前路由的方法由 `Route::getCurrentRoute()` 改為 `Route::current()`。

### Composer 更新

一旦你完成以上的更新，你可以執行 `composer update` 來更新應用程式的核心檔案。如果有 class load 錯誤，請在 `update` 之後加上 `--no-scripts`，如: `composer update --no-scripts`。

# 輔助方法

- [簡介](#introduction)
- [可用方法](#available-methods)

<a name="introduction"></a>
## 簡介

Laravel 包含一群多樣化的 PHP 輔助方法函式。許多在 Laravel 自身框架中使用；不過你也可以在自己的應用當中使用。
Laravel includes a variety of "helper" PHP functions. Many of these functions are used by the framework itself; however, you are free to use them in your own applications if you find them convenient.

<a name="available-methods"></a>
## 可用方法

<style>
    .collection-method-list > p {
        column-count: 3; -moz-column-count: 3; -webkit-column-count: 3;
        column-gap: 2em; -moz-column-gap: 2em; -webkit-column-gap: 2em;
    }

    .collection-method-list a {
        display: block;
    }
</style>

### 陣列

<div class="collection-method-list" markdown="1">
[array_add](#method-array-add)
[array_divide](#method-array-divide)
[array_dot](#method-array-dot)
[array_except](#method-array-except)
[array_first](#method-array-first)
[array_flatten](#method-array-flatten)
[array_forget](#method-array-forget)
[array_get](#method-array-get)
[array_only](#method-array-only)
[array_pluck](#method-array-pluck)
[array_pull](#method-array-pull)
[array_set](#method-array-set)
[array_sort](#method-array-sort)
[array_sort_recursive](#method-array-recursive)
[array_where](#method-array-where)
[head](#method-head)
[last](#method-last)
</div>

### 路徑

<div class="collection-method-list" markdown="1">
[app_path](#method-app-path)
[base_path](#method-base-path)
[config_path](#method-config-path)
[database_path](#method-database-path)
[elixir](#method-elixir)
[public_path](#method-public-path)
[storage_path](#method-storage-path)
</div>

### 字串

<div class="collection-method-list" markdown="1">
[camel_case](#method-camel-case)
[class_basename](#method-class-basename)
[e](#method-e)
[ends_with](#method-ends-with)
[snake_case](#method-snake-case)
[str_limit](#method-str-limit)
[starts_with](#method-starts-with)
[str_contains](#method-str-contains)
[str_finish](#method-str-finish)
[str_is](#method-str-is)
[str_plural](#method-str-plural)
[str_random](#method-str-random)
[str_singular](#method-str-singular)
[str_slug](#method-str-slug)
[studly_case](#method-studly-case)
[trans](#method-trans)
[trans_choice](#method-trans-choice)
</div>

### 網址

<div class="collection-method-list" markdown="1">
[action](#method-action)
[asset](#method-asset)
[secure_asset](#method-secure-asset)
[route](#method-route)
[url](#method-url)
</div>

### 其他

<div class="collection-method-list" markdown="1">
[auth](#method-auth)
[back](#method-back)
[bcrypt](#method-bcrypt)
[config](#method-config)
[csrf_field](#method-csrf-field)
[csrf_token](#method-csrf-token)
[dd](#method-dd)
[env](#method-env)
[event](#method-event)
[factory](#method-factory)
[method_field](#method-method-field)
[old](#method-old)
[redirect](#method-redirect)
[response](#method-response)
[value](#method-value)
[view](#method-view)
[with](#method-with)
</div>

<a name="method-listing"></a>
## 方法列表

<style>
    #collection-method code {
        font-size: 14px;
    }

    #collection-method:not(.first-collection-method) {
        margin-top: 50px;
    }
</style>

<a name="arrays"></a>
## 陣列

<a name="method-array-add"></a>
#### `array_add()` {#collection-method .first-collection-method}

如果給定的鍵不存在於該陣列，`array_add` 函式將給定的鍵值對加到陣列中：
The `array_add` function adds a given key / value pair to the array if the given key doesn't already exist in the array:

    $array = array_add(['name' => 'Desk'], 'price', 100);

    // ['name' => 'Desk', 'price' => 100]

<a name="method-array-divide"></a>
#### `array_divide()` {#collection-method}

`array_divide` 函式回傳兩個陣列，一個包含原本陣列的鍵，另一個包含原本陣列的值：
The `array_divide` function returns two arrays, one containing the keys, and the other containing the values of the original array:

    list($keys, $values) = array_divide(['name' => 'Desk']);

    // $keys: ['name']

    // $values: ['Desk']

<a name="method-array-dot"></a>
#### `array_dot()` {#collection-method}

`array_dot` 函式把多維陣列扁平化成一維陣列，並用「點」式語法表示深度：
The `array_dot` function flattens a multi-dimensional array into a single level array that uses "dot" notation to indicate depth:

    $array = array_dot(['foo' => ['bar' => 'baz']]);

    // ['foo.bar' => 'baz'];

<a name="method-array-except"></a>
#### `array_except()` {#collection-method}

`array_except` 函式從陣列移除給定的鍵值對：
The `array_except` method removes the given key / value pairs from the array:

    $array = ['name' => 'Desk', 'price' => 100];

    $array = array_except($array, ['price']);

    // ['name' => 'Desk']

<a name="method-array-first"></a>
#### `array_first()` {#collection-method}

`array_first` 函式回傳陣列中第一個通過為真測試的元素：
The `array_first` method returns the first element of an array passing a given truth test:

    $array = [100, 200, 300];

    $value = array_first($array, function ($key, $value) {
        return $value >= 150;
    });

    // 200

可傳遞第三個參數作為預設值。當沒有任何數值通過測試時將回傳該數值：
A default value may also be passed as the third parameter to the method. This value will be returned if no value passes the truth test:

    $value = array_first($array, $callback, $default);

<a name="method-array-flatten"></a>
#### `array_flatten()` {#collection-method}

`array_flatten` 函式將多維陣列扁平化成一維。
The `array_flatten` method will flatten a multi-dimensional array into a single level.

    $array = ['name' => 'Joe', 'languages' => ['PHP', 'Ruby']];

    $array = array_flatten($array);

    // ['Joe', 'PHP', 'Ruby'];

<a name="method-array-forget"></a>
#### `array_forget()` {#collection-method}

`array_forget` 函式以「點」式語法從深度巢狀陣列移除給定的鍵值對：
The `array_forget` method removes a given key / value pair from a deeply nested array using "dot" notation:

    $array = ['products' => ['desk' => ['price' => 100]]];

    array_forget($array, 'products.desk');

    // ['products' => []]

<a name="method-array-get"></a>
#### `array_get()` {#collection-method}

`array_get` 函式使用「點」式語法從深度巢狀陣列取回給定的值：
The `array_get` method retrieves a value from a deeply nested array using "dot" notation:

    $array = ['products' => ['desk' => ['price' => 100]]];

    $value = array_get($array, 'products.desk');

    // ['price' => 100]

`array_get` 函式同樣接受預設值，當指定的鍵找不到時回傳。
The `array_get` function also accepts a default value, which will be returned if the specific key is not found:

    $value = array_get($array, 'names.john', 'default');

<a name="method-array-only"></a>
#### `array_only()` {#collection-method}

`array_only` 函式從陣列回傳給定的鍵值對：
The `array_only` method will return only the specified key / value pairs from the given array:

    $array = ['name' => 'Desk', 'price' => 100, 'orders' => 10];

    $array = array_only($array, ['name', 'price']);

    // ['name' => 'Desk', 'price' => 100]

<a name="method-array-pluck"></a>
#### `array_pluck()` {#collection-method}

`array_pluck` 函式從陣列拉出一列給定的鍵值對：
The `array_pluck` method will pluck a list of the given key / value pairs from the array:

    $array = [
        ['developer' => ['name' => 'Taylor']],
        ['developer' => ['name' => 'Abigail']]
    ];

    $array = array_pluck($array, 'developer.name');

    // ['Taylor', 'Abigail'];

<a name="method-array-pull"></a>
#### `array_pull()` {#collection-method}

`array_pull` 函式從陣列移除並回傳給定的鍵值對：
The `array_pull` method returns and removes a key / value pair from the array:

    $array = ['name' => 'Desk', 'price' => 100];

    $name = array_pull($array, 'name');

    // $name: Desk

    // $array: ['price' => 100]

<a name="method-array-set"></a>
#### `array_set()` {#collection-method}

`array_set` 函式使用「點」式語法在深度巢狀陣列中寫入值：
The `array_set` method sets a value within a deeply nested array using "dot" notation:

    $array = ['products' => ['desk' => ['price' => 100]]];

    array_set($array, 'products.desk.price', 200);

    // ['products' => ['desk' => ['price' => 200]]]

<a name="method-array-sort"></a>
#### `array_sort()` {#collection-method}

`array_sort` 函式借由給定閉包結果排序陣列：
The `array_sort` method sorts the array by the results of the given Closure:

    $array = [
        ['name' => 'Desk'],
        ['name' => 'Chair'],
    ];

    $array = array_values(array_sort($array, function ($value) {
        return $value['name'];
    }));

    /*
        [
            ['name' => 'Chair'],
            ['name' => 'Desk'],
        ]
    */

<a name="method-array-sort-recursive"></a>
#### `array_sort_recursive()` {#collection-method}

`array_sort` 函式使用 `sort` 函式遞迴排序陣列：
The `array_sort_recursive` function recursively sorts the array using the `sort` function:

    $array = [
        [
            'Roman',
            'Taylor',
            'Li',
        ],
        [
            'PHP',
            'Ruby',
            'JavaScript',
        ],
    ];

    $array = array_sort_recursive($array);

    /*
        [
            [
                'Li',
                'Roman',
                'Taylor',
            ],
            [
                'JavaScript',
                'PHP',
                'Ruby',
            ]
        ];
    */

<a name="method-array-where"></a>
#### `array_where()` {#collection-method}

`array_where` 函式使用給定的閉包過濾陣列：
The `array_where` function filters the array using the given Closure:

    $array = [100, '200', 300, '400', 500];

    $array = array_where($array, function ($key, $value) {
        return is_string($value);
    });

    // [1 => 200, 3 => 400]

<a name="method-head"></a>
#### `head()` {#collection-method}

`head` 函式回傳給定陣列的第一個元素：
The `head` function simply returns the first element in the given array:

    $array = [100, 200, 300];

    $first = head($array);

    // 100

<a name="method-last"></a>
#### `last()` {#collection-method}

`last` 函式回傳給定陣列的最後一個元素：
The `last` function returns the last element in the given array:

    $array = [100, 200, 300];

    $last = last($array);

    // 300

<a name="paths"></a>
## 路徑

<a name="method-app-path"></a>
#### `app_path()` {#collection-method}

`app_path` 函式取得 `app` 資料夾的完整路徑：
The `app_path` function returns the fully qualified path to the `app` directory:

    $path = app_path();

你同樣可以使用 `app_path` 函式產生針對給定檔案相對於 app 目錄的完整路徑：
You may also use the `app_path` function to generate a fully qualified path to a given file relative to the application directory:

    $path = app_path('Http/Controllers/Controller.php');

<a name="method-base-path"></a>
#### `base_path()` {#collection-method}

`base_path` 函式取得專案根目錄的完整路徑：
The `base_path` function returns the fully qualified path to the project root:

    $path = base_path();

你同樣可以使用 `base_path` 函式產生針對給定檔案相對於專案根目錄的完整路徑：
You may also use the `base_path` function to generate a fully qualified path to a given file relative to the application directory:

    $path = base_path('vendor/bin');

<a name="method-config-path"></a>
#### `config_path()` {#collection-method}

`config_path` 函式取得應用設定目錄的完整路徑：
The `config_path` function returns the fully qualified path to the application configuration directory:

    $path = config_path();

<a name="method-database-path"></a>
#### `database_path()` {#collection-method}

`database_path` 函式取得應用資料庫目錄的完整路徑：
The `database_path` function returns the fully qualified path to the application's database directory:

    $path = database_path();

<a name="method-elixir"></a>
#### `elixir()` {#collection-method}

`elixir` 函式取得加上版本號的 [Elixir](/docs/{{version}}/elixir) 檔案路徑：
The `elixir` function gets the path to the versioned [Elixir](/docs/{{version}}/elixir) file:

    elixir($file);

<a name="method-public-path"></a>
#### `public_path()` {#collection-method}

`public_path` 函式取得 `public` 目錄的完整路徑：
The `public_path` function returns the fully qualified path to the `public` directory:

    $path = public_path();

<a name="method-storage-path"></a>
#### `storage_path()` {#collection-method}

`storage_path` 函式取得 `storage` 目錄的完整路徑：
The `storage_path` function returns the fully qualified path to the `storage` directory:

    $path = storage_path();

你同樣可以使用 `storage_path` 函式產生針對給定檔案相對於 storage 目錄的完整路徑：
You may also use the `storage_path` function to generate a fully qualified path to a given file relative to the storage directory:

    $path = storage_path('app/file.txt');

<a name="strings"></a>
## 字串

<a name="method-camel-case"></a>
#### `camel_case()` {#collection-method}

`camel_case` 函式轉換給定的字串成 ` 駝峰式命名 `：
The `camel_case` function converts the given string to `camelCase`:

    $camel = camel_case('foo_bar');

    // fooBar

<a name="method-class-basename"></a>
#### `class_basename()` {#collection-method}

`class_basename` 回傳給定類別不包含命名空間的類別名稱：
The `class_basename` returns the class name of the given class with the class' namespace removed:

    $class = class_basename('Foo\Bar\Baz');

    // Baz

<a name="method-e"></a>
#### `e()` {#collection-method}

`e` 函式對給定字串執行 `htmlentities`：
The `e` function runs `htmlentities` over the given string:

    echo e('<html>foo</html>');

    // &lt;html&gt;foo&lt;/html&gt;

<a name="method-ends-with"></a>
#### `ends_with()` {#collection-method}

`ends_with` 函式判斷給定字串結尾是否有指定內容：
The `ends_with` function determines if the given string ends with the given value:

    $value = ends_with('This is my name', 'name');

    // true

<a name="method-snake-case"></a>
#### `snake_case()` {#collection-method}

`snake_case` 函式轉換給定的字串成 ` 蛇形命名 `：
The `snake_case` function converts the given string to `snake_case`:

    $snake = snake_case('fooBar');

    // foo_bar

<a name="method-str-limit"></a>
#### `str_limit()` {#collection-method}

`str_limit` 函式限制字串的字元數量。該函式接受一個字串作為第一個參數，以及最大字元數量作為第二參數：
The `str_limit` function limits the number of characters in a string. The function accepts a string as its first argument and the maximum number of resulting characters as its second argument:

    $value = str_limit('The PHP framework for web artisans.', 7);

    // The PHP...

<a name="method-starts-with"></a>
#### `starts_with()` {#collection-method}

`starts_with` 函式判斷字串開頭是否為給定的內容：
The `starts_with` function determines if the given string begins with the given value:

    $value = starts_with('This is my name', 'This');

    // true

<a name="method-str-contains"></a>
#### `str_contains()` {#collection-method}

`str_contains` 函式判斷給定字串是否包含指定內容：
The `str_contains` function determines if the given string contains the given value:

    $value = str_contains('This is my name', 'my');

    // true

<a name="method-str-finish"></a>
#### `str_finish()` {#collection-method}

`str_finish` 函式添加給定內容到字串結尾：
The `str_finish` function adds a single instance of the given value to a string:

    $string = str_finish('this/string', '/');

    // this/string/

<a name="method-str-is"></a>
#### `str_is()` {#collection-method}

`str_is` 函式判斷字串是否符合給定模式。星號可作為萬用字元使用：
The `str_is` function determines if a given string matches a given pattern. Asterisks may be used to indicate wildcards:

    $value = str_is('foo*', 'foobar');

    // true

    $value = str_is('baz*', 'foobar');

    // false

<a name="method-str-plural"></a>
#### `str_plural()` {#collection-method}

`str_plural` 函式轉換字串成複數形。該函式目前僅支援英文：
The `str_plural` function converts a string to its plural form. This function currently only supports the English language:

    $plural = str_plural('car');

    // cars

    $plural = str_plural('child');

    // children

<a name="method-str-random"></a>
#### `str_random()` {#collection-method}

`str_random` 函式產生給定長度的隨機字串：
The `str_random` function generates a random string of the specified length:

    $string = str_random(40);

<a name="method-str-singular"></a>
#### `str_singular()` {#collection-method}

`str_singular` 函式轉換字串成單數形。該函式目前僅支援英文：
The `str_singular` function converts a string to its singular form. This function currently only supports the English language:

    $singular = str_singular('cars');

    // car

<a name="method-str-slug"></a>
#### `str_slug()` {#collection-method}

`str_slug` 函式從給定字串產生網址友善的「slug」：
The `str_slug` function generates a URL friendly "slug" from the given string:

    $title = str_slug("Laravel 5 Framework", "-");

    // laravel-5-framework

<a name="method-studly-case"></a>
#### `studly_case()` {#collection-method}

`studly_case` 函式轉換給定字串成 ` 首字大寫命名 `：
The `studly_case` function converts the given string to `StudlyCase`:

    $value = studly_case('foo_bar');

    // FooBar

<a name="method-trans"></a>
#### `trans()` {#collection-method}

`trans` 函式根據你的 [ 在地化檔案 ](/docs/{{version}}/localization) 翻譯給定的語句：
The `trans` function translates the given language line using your [localization files](/docs/{{version}}/localization):

    echo trans('validation.required'):

<a name="method-trans-choice"></a>
#### `trans_choice()` {#collection-method}

`trans_choice` 函式根據字尾變化翻譯給定的語句：
The `trans_choice` function translates the given language line with inflection:

    $value = trans_choice('foo.bar', $count);

<a name="urls"></a>
## 網址

<a name="method-action"></a>
#### `action()` {#collection-method}

`action` 函式產生給定控制器行為網址。你不需要輸入該控制器的完整命名空間。作為替代，請輸入基於 `App\Http\Controllers` 命名空間的控制器類別名稱：
The `action` function generates a URL for the given controller action. You do not need to pass the full namespace to the controller. Instead, pass the controller class name relative to the `App\Http\Controllers` namespace:

    $url = action('HomeController@getIndex');

如果該方法支援路由參數，你可以作為第二參數傳遞：
If the method accepts route parameters, you may pass them as the second argument to the method:

    $url = action('UserController@profile', ['id' => 1]);

<a name="method-asset"></a>
#### `asset()` {#collection-method}

Generate a URL for an asset using the current scheme of the request (HTTP or HTTPS):

	$url = asset('img/photo.jpg');

<a name="method-secure-asset"></a>
#### `secure_asset()` {#collection-method}

Generate a URL for an asset using HTTPS:

	echo secure_asset('foo/bar.zip', $title, $attributes = []);

<a name="method-route"></a>
#### `route()` {#collection-method}

`route` 函式產生給定路由名稱網址：
The `route` function generates a URL for the given named route:

    $url = route('routeName');

如果該路由接受參數，你可以作為第二參數傳遞：
If the route accepts parameters, you may pass them as the second argument to the method:

    $url = route('routeName', ['id' => 1]);

<a name="method-url"></a>
#### `url()` {#collection-method}

`url` 函式產生給定路徑的完整網址：
The `url` function generates a fully qualified URL to the given path:

    echo url('user/profile');

    echo url('user/profile', [1]);

<a name="miscellaneous"></a>
## 其他

<a name="method-auth"></a>
#### `auth()` {#collection-method}

`auth` 函式回傳一個認證器（authenticator）實例。你可以使用它取代 `Auth` facade：
The `auth` function return an authenticator instance. You may use it instead of the `Auth` facade for convenience:

    $user = auth()->user();

<a name="method-back"></a>
#### `back()` {#collection-method}

`back()` 函式產生一個重導回應（redirect response），返回使用者之前的位置：
The `back()` function generates a redirect response to the user's previous location:

    return back();

<a href="method-bcrypt"></a>
#### `bcrypt()` {#collection-method}

`bcrypt` 函式使用 Bcrypt 雜湊給定的數值。你可以使用它替代 `Hash` facade。
The `bcrypt` function hashes the given value using Bcrypt. You may use it as an alternative to the `Hash` facade:

    $password = bcrypt('my-secret-password');

<a name="method-config"></a>
#### `config()` {#collection-method}

`config` 取得設定選項的設定值。設定選項可透過「點」式語法讀取，其中包含要存取的檔名以及選項名稱。可傳遞一預設值在找不到指定的設定選項時回傳該數值：
The `config` function gets the value of a configuration variable. The configuration values may be accessed using "dot" syntax, which includes the name of the file and the option you wish to access. A default value may be specified and is returned if the configuration option does not exist:

    $value = config('app.timezone');

    $value = config('app.timezone', $default);

The `config` helper may also be used to set configuration variables at runtime by passing an array of key / value pairs:

    config(['app.debug' => true]);

<a name="method-csrf-field"></a>
#### `csrf_field()` {#collection-method}

`csrf_field` 函式產生包含 CSRF 標記內容的 HTML 表單隱藏欄位。例如，使用 [Blade 語法 ](/docs/{{version}}/blade)：
The `csrf_field` function generates an HTML `hidden` input field containing the value of the CSRF token. For example, using [Blade syntax](/docs/{{version}}/blade):

    {!! csrf_field() !!}

<a name="method-csrf-token"></a>
#### `csrf_token()` {#collection-method}

`csrf_token` 函式取得當前 CSRF 標記的內容：
The `csrf_token` function retrieves the value of the current CSRF token:

    $token = csrf_token();

<a name="method-dd"></a>
#### `dd()` {#collection-method}

`dd` 函式印出給定變數並結束腳本執行：
The `dd` function dumps the given variable and ends execution of the script:

    dd($value);

<a name="method-env"></a>
#### `env()` {#collection-method}

`env` 函式取得環境變數值或回傳預設值：
The `env` function gets the value of an environment variable or returns a default value:

    $env = env('APP_ENV');

    // Return a default value if the variable doesn't exist...
    $env = env('APP_ENV', 'production');

<a name="method-event"></a>
#### `event()` {#collection-method}

`event` 函式配送給定 [ 事件 ](/docs/{{version}}/events) 到所屬的監聽器：
The `event` function dispatches the given [event](/docs/{{version}}/events) to its listeners:

    event(new UserRegistered($user));

<a name="method-factory"></a>
#### `factory()` {#collection-method}

`factory` 函式根據給定類別、名稱以及總數產生模型工廠建構器（model factory builder）。可用於 [ 測試 ](/docs/{{version}}/testing#model-factories) 或 [ 資料填充 ](/docs/{{version}}/seeding#using-model-factories)
The `factory` function creates a model factory builder for a given class, name, and amount. It can be used while [testing](/docs/{{version}}/testing#model-factories) or [seeding](/docs/{{version}}/seeding#using-model-factories):

    $user = factory(App\User::class)->make();

<a name="method-method-field"></a>
#### `method_field()` {#collection-method}

`method_field` 函式產生擬造 HTTP 表單動作內容的 HTML 表單隱藏欄位。例如，使用 [Blade 語法 ](/docs/{{version}}/blade)：
The `method_field` function generates an HTML `hidden` input field containing the spoofed value of the form's HTTP verb. For example, using [Blade syntax](/docs/{{version}}/blade):

    <form method="POST">
        {!! method_field('delete') !!}
    </form>

<a name="method-old"></a>
#### `old()` {#collection-method}

`old` 函式 [ 取得 ](/docs/{{version}}/requests#retrieving-input) 快閃到 session 的舊有輸入數值：

    $value = old('value');

<a name="method-redirect"></a>
#### `redirect()` {#collection-method}

`redirect` 函式回傳 redirector 實例以進行 [ 重導 ](/docs/{{version}}/responses#redirects)：
The `redirect` function return an instance of the redirector to do [redirects](/docs/{{version}}/responses#redirects):

    return redirect('/home');

<a name="method-response"></a>
#### `response()` {#collection-method}

`response` 函式建立一個 [ 回應 ](/docs/{{version}}/responses) 實例或獲取一個回應工廠（response factory）實例：
The `response` function creates a [response](/docs/{{version}}/responses) instance or obtains an instance of the response factory:

    return response('Hello World', 200, $headers);

    return response()->json(['foo' => 'bar'], 200, $headers);

<a name="method-value"></a>
#### `value()` {#collection-method}

`value` 函式的行為將回傳給定數值。而當你傳遞一個 ` 閉包 ` 給該函式，該 ` 閉包 ` 將被執行並回傳結果：
The `value` function's behavior will simply return the value it is given. However, if you pass a `Closure` to the function, the `Closure` will be executed then its result will be returned:

    $value = value(function() { return 'bar'; });

<a name="method-view"></a>
#### `view()` {#collection-method}

`view` 函式取得 [ 視圖 ](/docs/{{version}}/views) 實例：
The `view` function retrieves a [view](/docs/{{version}}/views) instance:

    return view('auth.login');

<a name="method-with"></a>
#### `with()` {#collection-method}

`with` 函式回傳給定的數值。該函式主要用於方法鍊結（method chaining），除此之外不太可能用到。
The `with` function return the value it is given. This function is primarily useful for method chaining where it would otherwise be impossible:

    $value = with(new Foo)->work();

### Controllers

Controllers are an alternative to Closures for defining the application logic

Generating a new Controller

`php artisan make:controller ControllerNameController`

Controllers are stored inside the `app/Http/Controllers` folder

An example controller class

```php
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;

class HomeController extends Controller
{
    public function index()
    {
        return view('home');
    }
    
    public function contact()
    {
        return view('contact');
    }
}
```

Controllers do not have to extend the base `App\Http\Controllers\Controller` class, but it provides some convienience methods.

Route definition for the above controller (routes/web.php):

```php
Route::get('/', 'HomeController@home');
Route::get('/contact', 'HomeController@contact');

```

We don't have to specify the full controller namespace in `web.php`. It's enough to specify everything after `App\Http\Controllers`.

RouteServiceProvider will is responsible for prepending the `App\Http\Controllers` namespace to controller names in routes.

### Single Action Controllers

For controllers that handle just a single action:

```php
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;

class HomeSingleController extends Controller
{
    public function __invoke()
    {
        return view('home');
    }
}
```

Route definition (routes/web.php)

```php
Route::get('home', 'HomeSingleController');
```

Generating a single action controller

`php artisan make:controller HomeSingleController --invokable`

The `__invoke` is a magic PHP method that allows the object to be called like a function, eg.

```php
$controller = new HomeSingleController();
$controller();
```

Of course you would never create controller classes yourself, Laravel handles that. This is just an example of how invokable object (object that can be called like it would be a function) in PHP looks like.

### Routing

Route for controller action

```
$url = action('HomeController@home');
```

### Testing

You are already set up with Laravel to test your application.

By default, tests are stored inside `tests` directory.

It contains two further ones:

* `Unit` - for testing small isolated parts of your code, like one class functionality or a single method
* `Feature` - as name suggests, testing features of your app, often through making HTTP requests to your running application

The configuration file `phpunit.xml` is already included.

#### Testing in a separate environment

Tests usually run in a separate `environment`. By `environment` I mean different set of settings for your application.

As you normally store your environment variables inside `.env` file for local development, you would configure this variables inside `phpunit.xml` file instead.

By default, Laravel runs tests in `testing` environment.

If your tests involve database, you would not like to perform any changes on your local database.

You might create a new MySQL database for testing, or use SQLite (an in-memory version of it).

To specify a different database connection for testing environment, add

```xml
<env name="DB_CONNECTION" value="sqlite_testing" />
```

Inside the `phpunit.xml`.

Then, configure the connection inside `config/database.php` file like below

```php
'sqlite_testing' => [
    'driver' => 'sqlite',
    'database' => ':memory:'
],
```

The above example would define a new `sqlite_testing` connection, using SQLite.
To create this database in memory, we use the special `database` property value `:memory:`

Important, before running your tests for the first time, run

`php artisan config:clear`

To clear configuration cache. Read more about [configuration cache](https://laravel.com/docs/7.x/configuration#configuration-caching).

#### Running tests

To run tests

`./vendor/bin/phpunit`

#### Writing tests

All your tests will extend the base class `TestCase` from `Tests` namespace.

Here is an example `Unit` test

```php
<?php

namespace Tests\Unit;

use Tests\TestCase;

class ExampleTest extends TestCase
{
    public function testBasicTest()
    {
        $this->assertTrue(true);
    }
}
```

All testing method names should start with `test`, eg. `testHome`, `testContact`, `testPostStored` etc.

A single test can be divided into three parts

* `Arrange` - test set up, like creating an object to be tested or mocks
* `Act` - execute the objects created in the `Arrange` step
* `Assert` - check and verify the result from the `Act` step against expected results

#### Database

To refresh database after each test (rebuild schema using migrations), add the `Illuminate\Foundation\Testing\RefreshDatabase` trait to your test class.

An example:

```php
<?php

namespace Tests\Feature;

use App\BlogPost;
use Tests\TestCase;
use Illuminate\Foundation\Testing\RefreshDatabase;

class PostTest extends TestCase
{
    use RefreshDatabase;

    public function testPostIndex()
    {
        $response = $this->get('/posts');

        $response->assertSeeText('No blog posts yet!');
    }
}
```

#### Testing using HTTP requests

You can call your application using HTTP 

```php
$response = $this->get('/posts');
```

Then, you can perform some assertions on the result, like checking if certain text was displayed or if JSON with specific values was returned.

```php
$response->assertSeeText('First post');
```

Here is a list of all [possible assertions](https://laravel.com/docs/7.x/http-tests#available-assertions)


### Inside route definition file (routes/web.php)

Defining a route using closure

```
Route::get('/', function () {
    return view('welcome');
});
```

Defining a route that only renders a Blade template

```
Route::view('/home')
Route::view('/home', ['data' => 'value'])
```

Route with a required parameter

```
Route::get('/page/{id}', function ($id) {
    return view('page', ['page' => $id]);
});
```

Route with an optional parameter

```
Route::get('/hello/{name?}', function ($name = 'Guest') {
    return view('hello', ['name' => $name]);
});
```

### Inside Blade template
Defining a section

```
@section('content')
	<h1>Header</h1>
@endsection
```
Rendering a section

`@yield('content')`

Extending a layout

`@extends('layout')`

Function to render a view

`view('name', ['data' =>‚ 'value'])`

Rendering data inside a Blade template

`{{ $data }}`

*By default data is escaped using `htmlspecialchars`*

Rendering unescaped data

`{{ !! $data !! }}`

Including another view

`@include('view.name')`

*Included view will inherit parent view data*

Passing additional data to included view

`@include('view.name', ['name' => 'John'])`

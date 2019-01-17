###Inside route definition file (routes/web.php)

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

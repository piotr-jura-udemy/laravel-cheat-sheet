### Loops and including partial templates

Iterating over elements of collection or array

```blade
@foreach ($posts as $post)
	{{ $post->title }}
@endforeach
```

Iterating over elements of collection or array and rendering a value when collection is empty (zero length)

```blade
@forelse ($posts as $post)
	{{ $post->title }}
@empty
	<p>No blog posts</p>
@endforelse
```

Including a sub-view (included views inherit the data of parent view)

```blade
@include('post')
```
Passing additional data to included view

```blade
@include('post', ['some' => 'data'])
```

Including multiple views at once for a collection

```blade
@each('post', $posts, 'post')
```

The first argument is the partial view template name, second the collection, third the variable name that would be available inside included view

### Conditional rendering

The @if directive

```blade
@if ($post->id === 1)
    Post one!
@elseif ($post->id === 2)
    Post two!
@else
    Something else
@endif
```

The @unless directive

```blade
@unless ($post->id === 1)
    Post one!
@endunless
```


### Dates

#### Date mutators

[https://laravel.com/docs/5.3/eloquent-mutators#date-mutators](https://laravel.com/docs/5.3/eloquent-mutators#date-mutators)

By default the `created_at` and `updated_at` will be converted to Carbon date objects

It can be configured using `dates` field of the model

```blade
class BlogPost extends Model
{
    protected $dates = [
        'created_at',
        'updated_at',
        'deleted_at'
    ];
}
```

#### Date format

By default date columns are stored as `Y-m-d H:i:s` format

It can be customized using `dateFormat` field of the model.

**Warning!** This will change how date is stored inside the database and how it is being formatted by default!

```blade
class BlogPost extends Model
{
    protected $dateFormat = 'Y-m-d';
}
```

#### Carbon

Carbon is a PHP library that extends the base `\DateTime` class. It's extensively used in Laravel. 

Full API documentation [https://carbon.nesbot.com/docs/](https://carbon.nesbot.com/docs/)

Formatting the date in the "time ago" format (in Blade template)

```blade
{{ $post->created_at->diffForHumans() }}
```

Checking for time difference (https://carbon.nesbot.com/docs/#api-difference)

In the below example we check if the time passed between now, and the post created_at date is less than 5 minutes. Only then we render the "New!" badge.

```blade
@unless ((new Carbon\Carbon())->diffInMinutes($post->created_at) < 5)
    <strong>New!</strong>
@endunless
```

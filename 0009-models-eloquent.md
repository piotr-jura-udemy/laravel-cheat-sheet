### Laravel Tinker

Tinker is a console program that allows you to play around with Laravel models and execute arbitraty PHP command directly from your command line

Starting the console

```
php artisan tinker
```

#### Solving a problem with Tinker (for PHP 7.3 or newer) when it quits after every command

Modify the php.ini by adding this option

```
pcre.jit=0
```

On Mac php.ini can be usually found in `/Applications/XAMPP/xamppfiles/etc/php.ini`

To be sure where it is, run `php -i | grep 'php.ini'` in Terminal

On Windows it's in your XAMPP folder `C:\xampp\php\php.ini` or `C:\xampp\etc\php.ini`, depending on location of XAMPP itself


### Eloquent Model

Generating a new model

```
php artisan make:model BlogPost
```

Generating a new model with migration

```
php artisan make:model BlogPost --migration
// or
php artisan make:model BlogPost -m
```

By convention, Laravel assumes the table name is "snake case" plural model name. For example:

| Model name                           | Table name                                              |
| --------                          |-------------                                             |
| BlogPost       | blog_posts                                                                   
| Blogpost		| blogposts

To define a custom name, add (override) the protected `$table` model property

```
class BlogPost extends Model
{
    protected $table = 'blogposts';
}
```

By default, all models are stored inside the `App` namespace, eg. `App\BlogPost`

#### Acessing and modifying properties

You can read and modify model properties (row columns) using properties

```
$post = App\BlogPost::find(1);
$title = $post->title;
$content = $post->content;

$post->title = 'New title';
$post->content = 'New content';
// Always call save() to create the record and UPDATE the existing one
$post->save();
```

Property name corresponds 1:1 to the column name of the table

### Querying

Retrieving all models as *collection*

```
$posts = App\BlogPost::all();
```

Retrieving single model by primary key (usually, by `id` property/column)

```
// Fetch BlogPost with id 10
$post = App\BlogPost::find(10);
```

Fetching *collection* of models by id

```
$posts = App\BlogPost::find([1, 2, 3]);
```

Collections are iterable (eg. using foreach)

```
$posts = App\BlogPost::all();

foreach ($posts as $post) {
	echo $post->title;
}
```

Getting first element of the collection of models

```
$posts = App\BlogPost::all();
$post = $posts->first();
```

Creating and saving (creating a database row) a new model

```
$post = new App\BlogPost();
$post->title = 'Title';
$post->content = 'Content';
$post->save();
```
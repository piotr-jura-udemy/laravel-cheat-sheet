### Migrations problems

The limit for keys is 767 bytes.

In the `utf-8` encoding, the single character is 3 bytes, so key on `VARCHAR(255)` length won't exceed 767 (3 * 255 = 765).

In you are using `utf8mb4`, which we are, the single character is 4 bytes. Thus the maximum length for `VARCHAR` which has key on it (like `UNIQUE`) is 191.

When you encounter this:

```
Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table

Illuminate\Database\QueryException  : SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQL: alter table `users` add unique `users_email_unique`(`email`))
```

Change the email field length to 191.

### Running migrations

To run the most recent, not executed yet migrations

```
php artisan migrate
```

To rollback the most recent migration

```
php artisan migrate:rollback
```

Setting the length of the field

```
$table->string('email', 191);
```

### Writing migrations

Creating a new migration

```
php artisan make:migration create_blogposts_table
```

To prefill the migration with stub code that creates a new table

```
php artisan make:migration create_blogposts_table --create=blogposts
```

To prefill the migration with stub code that modifies an existing table


```
php artisan make:migration add_date_to_blogposts_table --table=blogposts
```

### The migration file

Migration file containts a class with 2 methods, `up()` and `down()`

The `up()` methods creates new table, modifies the existing one. Generally, it specifies how your database schema should change from now on - this might include deleting fields or tables.

The `down()` method specifies how to revert changes made my migration.

`up()` method is called when you run `php artisan migrate`

`down()` method is called when you run `php artisan migrate:rollback`

Creating a new table

```
Schema::create('blogposts', function (Blueprint $table) {
    $table->increments('id');
});
```

Renaming an existing table

```
Schema::rename('blogposts', 'posts');

```

Creating columns

```
Schema::table('blogposts', function (Blueprint $table) {
    $table->string('title');
});
```

Available column types

Refer to this link [https://laravel.com/docs/5.7/migrations#columns](https://laravel.com/docs/5.7/migrations#columns)

Typical columns types

| Command                           | Description                                              |
| --------                          |-------------                                             |
| `$table->increments('id');`       | Auto-incrementing UNSIGNED INTEGER                       |
| `$table->string('title', 100);`   | VARCHAR with optional length                             |
| `$table->timestamps();`           | Nullable TIMESTAMP `created_at` and `updated_at` columns |
| `$table->text('content');`        | TEXT                                                     |

Column modifiers

`->default('value')` - the default column value

`->nullable()` - column can be NULL

`->unsigned()` - integer is unsigned (no negative values)
### Migrations problems

The limit for keys is 767 bytes.

In the `utf-8` encoding, the single character is 3 bytes, so key on `VARCHAR(255)` length won't exceed 767 (3 * 255 = 765).

In you are using utf8mb4, which we are, the single character is 4 bytes. Thus the maximum length for VARCHAR which has key on it (like `UNIQUE`) is 191.

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

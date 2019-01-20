### Configuring database

The database connection parameters are stored inside .env file (on development environment).

On production environment store it in VirtualHost configuration or .htaccess file. To store variables in .htaccess file VirtualHost must contain the `AllowOverride All` directive.

Reading environment variable

```
$value = env('DB_HOST', '127.0.0.1');
```

*Where first value is the name of the variable, and second is the default value (if env variable is not defined).*

### Connecting to the database server

#### Using phpMyAdmin

Visit [http://localhost/phpmyadmin](http://localhost/phpmyadmin) if you are using XAMPP

Create a new database

![Creating database in phpMyAdmin](./0005-create-database.gif)
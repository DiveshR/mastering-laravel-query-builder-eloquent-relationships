# mastering-laravel-query-builder-eloquent-relationships

## Migrations

#### Create New Laravel Project
```
laravel new laraveldb
```
##### Laravel Supports following Databases:
Mysql,mariadb,postgressql,sqlite and sql server

##### Laravel artisan command to show list of databases:
````
php artisan db:show
````
##### Show another database connected.
````
php artisan db:show --database=pgsql
````
##### In config folder we have 15 configuration file
database.php

Migrations allow you to modify your database schema using php code instead of sql.
###### 1st way
`````
php artisan make:migration "create posts table"
`````
###### 2st way
`````
php artisan make:migration create_posts_table
`````
Migrations allow you to design a database schema before using it.
Migration file ```return instance of a migration class in migration table```
schema --comes from schema builder class.
closure parameter of Blueprint object

##### Creating Migrations :
Datatypes commonly used:
```````
string()
text()
longText()
boolean()
integer()
float()
````````

##### Column Modifiers :
Laravel has total ````18 columns```` modifiers

###### 1. Unique()
###### Before
`````
$table->string('name');
`````
###### After
`````
$table->string('name')->unique();
`````
###### Alter ways
`````
$table->string('name')->unique();
``````
1.  ```$table->unique('name');```
2. When more than 1 column is unique ```$table->unique(['name',''email]);```

###### Before
`````
$table->string('name');
`````
###### After
`````
$table->string('name')->unique();
`````
###### Alter ways
`````
$table->string('name')->unique();
``````
1.  ```$table->unique('name');```
2. When more than 1 column is unique ```$table->unique(['name',''email]);```

###### 2. comment();
```
$table->boolean('status')->comment('Status of a user');
```

###### 3. default();
```
$table->boolean('status')->default(false);
```
###### 4. from();
- id column has auto-increment value with 1, But if you want it to start from a particular value we use ```from()```.

```
$table->id()->from(1000);
```
###### 5. nullable();
- When we no  need value to a column, we uses ```nullable()```





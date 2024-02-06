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


### Running Migrations
###### 1. Migrate all tables
```
php artisan migrate
```
###### 2. The status artisan command shows us migration history
```
php artisan migrate:status
```
###### 2. The status artisan command shows us migration history
```
php artisan migrate:status
```
###### 3. The  --pretend flag allow us to see the full SQL statement of your migration.
```
php artisan migrate --pretend
```
###### 4. The  reset command Rollback all of your migrations or simply remove the database tables.
```
 php artisan migrate:reset 
```
###### 5.  The  force flag allow us to overwrite the current tables.
```
php artisan migrate —force 
```
###### 6. The rollback command rollbacks the last migration.
```
php artisan migrate:rollback
```
###### 7. The step flag allow user to rollbacks last n no of migration.
```
php artisan migrate:rollback —-step=n
```
###### 8. The refresh command performs two operations it first delete migrations and migrate all tables again  i.e up operation. Simply it first delete all tables from database and again fill the tables into the database.
```
php artisan migrate:refresh
```
###### 9. The refresh command with step flags performs two operations it first delete last n no of migrations and migrate then migrate all pending migrations  i.e up operation.
```
php artisan migrate:refresh —-step=2 
```
###### 10. The fresh command performs two operations it first perform down operation in migrations and then migrate all tables again.
```
php artisan migrate:fresh
```
NOTE: MAIN DIFFERENCE BETWEEN fresh and refresh COMMAND IS REFRESH COMMAND DELETE ALL TABLES AND THEN PERFORM UP OPERATION FOR MIGRATION, BUT FRESH COMMAND FIRST RUNS DOWN OPERATION TO DELETE ALL TABLES FROM DATABASE AND THEN PERFORMS UP OPERATION FOR MIGRATE ALL TABLES INTO THE DATABASE. 



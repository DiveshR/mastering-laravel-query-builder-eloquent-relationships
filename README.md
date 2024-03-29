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

### Squashing Migrations :
###### The schema dump artisan command generate a SQL file of your database. Which will be saved inside schema directory under database directory(database/schema directory).
```
php artisan schema:dump
```
###### The schema dump artisan command with prune flag will dump the current database schema and prune all existing migrations
```
php artisan schema:dump --prune
```

### Modifying Columns : 
###### The make migration artisan command with --table flag with table name helps us to add new column to a existing table.
```
php artisan make:migration add_country_in_users_table --table=users 
```
```
    public function up(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->string('country');
        });
    }

```
Another example which modify the existing column 

```
Schema::table('users', function (Blueprint $table) {
    $table->string('name', 50)->change();
});
```
When modifying a column, you must explicitly include all of the modifiers you want to keep on the column definition - any missing attribute will be dropped. For example, to retain the unsigned, default, and comment attributes, you must call each modifier explicitly when changing the column:

```
Schema::table('users', function (Blueprint $table) {
    $table->integer('votes')->unsigned()->default(1)->comment('my comment')->change();
});
```
```
Schema::table('users', function (Blueprint $table) {
    $table->string('name', 50)->change();
});
```
### Renaming Columns : 
Rename ```country``` column to ```country_id```
```
php artisan make:migration rename_country_to_country_name_on_users_table --table=users
```
```
    public function up(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->renameColumn('country', 'country_name');
        });
    }
Then run ```php artisan migrate```
```

NOTE: While renaming column renameColumn required two parameter from and to where from is older column name and to is new column name.

### Dropping Columns : 
To drop a column, you may use the ```dropColumn()``` method on the schema builder:
```
Schema::table('users', function (Blueprint $table) {
    $table->dropColumn('name');
});
```

For Deleting multiple columns : 
```
Schema::table('users', function (Blueprint $table) {
    $table->dropColumn(['name','age','city']);
});
```
###### Available Command Aliases:
```
$table->dropMorphs('morphable');
// Drop the morphable_id and morphable_type columns.
```
```
$table->dropRememberToken();
// Drop the remember_token column.
```

```
$table->dropSoftDeletesTz();
// Alias of dropSoftDeletes() method.
```

```
$table->dropTimestamps();
// Drop the created_at and updated_at columns.
```

```
$table->dropTimestampsTz();
// Alias of dropTimestamps() method.
```

### Foreign Key Constraints : 
Laravel also provides support for creating foreign key constraints, which are used to force referential integrity at the database level.
For example, let's define a ```user_id``` column on the ```posts``` table that references the ```id``` column on a ```users``` table:

```
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
 
Schema::table('posts', function (Blueprint $table) {
    $table->unsignedBigInteger('user_id');
 
    $table->foreign('user_id')->references('id')->on('users');
});
```

Since this syntax is rather verbose, Laravel provides additional, terser methods that use conventions to provide a better developer experience. When using the foreignId method to create your column, the example above can be rewritten like
```
Schema::table('posts', function (Blueprint $table) {
    $table->foreignId('user_id')->constrained();
});
```

You may also specify the desired action for the "on delete" and "on update" properties of the constraint:
```
$table->foreignId('user_id')
      ->constrained()
      ->onUpdate('cascade')
      ->onDelete('cascade');

```
```
$table->cascadeOnUpdate();
// Updates should cascade.
```
```
$table->restrictOnUpdate();
// Updates should be restricted.
```
```
$table->noActionOnUpdate();
// No action on updates.
```

```
$table->cascadeOnDelete();
// Deletes should cascade.
```
```
$table->restrictOnDelete();
// Deletes should be restricted.
```
```
$table->nullOnDelete();
// Deletes should set the foreign key value to null.
```

Any additional column modifiers must be called before the constrained method:

```
$table->foreignId('user_id')
      ->nullable()
      ->constrained();
```

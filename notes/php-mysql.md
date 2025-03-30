# 582-database-integration

Simple php / mysql database integration example

## Download Sample Files

[Download php / mysql sample files here.](../code-sample/php-mysql.zip)

---

## Setup a database on plesk

Simple database integration example, if you want to jump ahead, go to the [integrate](#integrate-the-database-in-php) section.

### Log-in on plesk and in `Dashboard` select `Databases`

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.45.21 PM.jpg>)

### Click on `+ Add Database`

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.46.04 PM.jpg>)

### Set your `Database name`, `Database user name` and `Password`

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.46.32 PM.jpg>)

### Once your database is created, you can select `phpMyAdmin`

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.46.45 PM.jpg>)

### Create a database inside phpMyAdmin

### Once you opened phpMyAdmin, you should see `Create new table` option, add the `Table name` and change the `Number of columns` to match the different sets of data. (You can always add more later)

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.47.09 PM.jpg>)

### Add the `Name` of your fields and select the `type`

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.47.36 PM.jpg>)

### Note: `ID` should always be your first field and it should be of type `INT` (integer) and make sure you `check` the `A_I` (auto increment) option to set the ID as your `PRIMARY` key

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.48.02 PM.jpg>)

### For any fields that needs alphabet characters, chose `VARCHAR` (variable characters)

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.48.51 PM.jpg>)

### Change the length for each of the fields, default for `INT` with `PRIMARY` key will automatically be set to `11` in length

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.49.31 PM.jpg>)

### Click on `Save` to add the table, or `Preview SQL` to preview your command

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.49.42 PM.jpg>)

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.49.51 PM.jpg>)

### Once you have created your table, you will be presented with your table's structure

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.50.08 PM.jpg>)

### You can select your new table on the left side menu and you will see the `Browser` tab open with the default `SELECT *` command

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 3.51.01 PM.jpg>)

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.01.03 PM.jpg>)

### You can select the `Insert` tab

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.01.21 PM.jpg>)

### Add a new entry, make sure you **_do not_** add anything to the ID field, or else your entries will have duplicate primary key. Click `Go` when you are ready to add an entry

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.02.02 PM.jpg>)

### Once the entry is added, you will see `1 row inserted` and the new row `id` along with the SQL command that was just executed

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.02.14 PM.jpg>)

### If you click on `Go` again, it will execute the code again

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.02.18 PM.jpg>)

### If you did, you will see the execution message again

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.02.27 PM.jpg>)

### Click on `Browse` to see the results

<!-- ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.02.35 PM.jpg>) -->

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 4.02.48 PM.jpg>)

---

## Integrate the database in php

Note: **Read carefully** any errors when you **access the php page directly**.

### Add connection information in `php/db_connect.php`

Open [`php/db_connect.php`](template/php/db_connect.php) and change the `$user`, `$pass` and `$db` information to match the information from the [setup](#setup-a-database-on-plesk) page.

| Variable | Description |
| -- | -- |
| `$db` | database name |
| `$user` | database user name |
| `$pass` | password |

![Alt text](<../img/php-mysql/Screenshot 2025-03-30 at 7.12.13 PM.jpg>)

### Edit select information in `php/select.php`

When reading (not writing) from the database, you will have to execute a `SELECT` command.
Open [`php/select.php`](template/php/select.php), there will be 3 spots to change information.

1. On `line 13`, edit `SELECT` statement to reference the table you wish to select.
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.24.14 PM.jpg>)
2. On `line 27`, make sure you **match the number of `$field` variables** to match the number of expected fields from the database.
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.24.28 PM.jpg>)
3. On `line 32`, edit the output array varibales to **match the number of `$field` variables** and the **expected output names** (names on the left side of the `=>`, the right side ones doesn't matter as much, it just have to match the same ones from step 2).
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.24.43 PM.jpg>)

### Edit insert information in `php/insert.php`

When writing to the database, you will have to execute an `INSERT` command.
Open [`php/insert.php`](template/php/insert.php), there will be 3 spots to change information.

1. On `line 13`, edit `INSERT` statement to reference the table you wish to select.
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.21.23 PM.jpg>)
2. On the same line, edit **the names and number of `$field` variables and `?` that follows** to match the field names **_from the database_** to be inserted to.
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.19.24 PM.jpg>)
3. On `line 22`, update the **bind parameter types and variables** to match the field names **_from the form_** that is sending the data to this page.
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.18.59 PM.jpg>)
   ![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.23.14 PM.jpg>)

---

## Interface to php from javascript

There are two `HTML` files that has accompanying `js` files that function to access the `php` files on the server to interface with the database from the user end.

You should not need to change anything from the templates, but if you edit form names or the id of the viewer in the `html` files, make sure they are also changed on the `js` files.

The namse are located on `line 1` for both the [js/form.js](template/js/form.js) and the [js/view.js](template/js/view.js) files.

![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.26.20 PM.jpg>)
![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.16.04 PM.jpg>)
![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.26.31 PM.jpg>)
![Alt text](<../img/php-mysql/Screenshot 2023-10-01 at 9.16.14 PM.jpg>)

The `js` files use the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to request data from an API or send data via [FormData](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#body).

**Note:** If you want to see more how endpoints work, visit [https://sampleapis.com/](https://sampleapis.com/).

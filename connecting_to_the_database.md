# PDO - PHP Data Objects
PDO is a database access layer providing a uniform method of access to multiple databases in PHP. It is a database abstraction layer that allows developers to interact with databases using a consistent set of functions, regardless of the underlying database system. 

PDO supports various database drivers, making it a versatile and portable solution for database connectivity in PHP. It provides a secure and efficient way to connect to databases, execute queries, and fetch results. PDO also helps prevent SQL injection by supporting parameterized queries, enhancing the overall security of database interactions in PHP applications.

# Connecting to the database
Database connections can live inside an include. So the file can be reused everytime it is needed.
### database-connection.php
```php
<?php

$type = 'mysql'; // Type of database
$server = 'localhost'; // Server the database is on
$db = 'your-db'; // Name of the database
$port = ''; // Port is usually 8889 in MAMP and 3306 in XAMPP
$charset = 'utf8mb4'; // UTF-8 encoding using 4 bytes of data per character

$username = 'root'; // Enter YOUR username here
$password = ''; // Enter YOUR password here

$options = [ // Options for how PDO works
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
]; // Set PDO options

$dsn = "$type:host=$server;dbname=$db;port=$port;charset=$charset"; // Create DSN
try { // Try following code
    $pdo = new PDO($dsn, $username, $password, $options); // Create PDO object
} catch (PDOException $e) { // If exception thrown
    throw new PDOException($e->getMessage(), $e->getCode());  // Re-throw exception
}

?>
```
### Get one row of data from a database
```php
<?php
require '../cms/includes/database-connection.php';
$sql = "SELECT forename, surname
        FROM member
        WHERE id = 1;";
$statement = $pdo->query($sql);
$member = $statement->fetch();
?>
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Getting one row of data from a database</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css" />
  </head>
  <body>
    <p>
      <?= html_escape($member['forename']) ?>
      <?= html_escape($member['surname']) ?>
    </p>
  </body>
</html>
```

### Get multiple rows of data from a database
```php
<?php
require '../cms/includes/database-connection.php';
require '../cms/includes/functions.php';
$sql = "SELECT forename, surname FROM member;";
$statement = $pdo->query($sql);
$members   = $statement->fetchAll();
?>
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Getting multiple rows of data from the database</title>
  </head>
  <body>
    <?php foreach ($members as $member) { ?>
      <p>
        <?= html_escape($member['forename']) ?>
        <?= html_escape($member['surname']) ?>
      </p>
    <?php } ?>
  </body>
</html>
```


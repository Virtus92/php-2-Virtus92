# Using a single file to display many pages
When a single PHP file is used to display many pages of a site, a query string can be added to the URL to tell the PHP file which data it needs to collect from the database.

A PHP page can collect a value from a query string and then use that value in a SQL query to specify what data should be collected from the database.

Below, the link to member.php has a query that holds the name **id** and a **value** of 1. This corresponds to the id column of the member table in the database.
```html
<a href="member.php?id=1">Ivy Stone</a>
```
The member.php page uses PHP's filter_input() function to get the value from the query string. 
```php
    $id = filter_input(INPUT_GET, 'id', FILTER_VALIDATE_INT);
    //if the id is not valid, show a page not found 
    if(!$id){
        include 'page-not-found.php';
    }
```
Because the id columns in the database are all integers, the function uses the integer filter. The value it returns is stored in a variable called $id:
- If it's an integer, $id will hold that integer.
- If it's not an integer, $id will hold false.
- If id is not in the query string, $id will hold null.

If the query string did contain a valid integer, the page can continue to try and get data from the database and store it in a variable.

### Complete Example
```php
<?php
require '..database-connection.php';

$id = filter_input(INPUT_GET, 'id', FILTER_VALIDATE_INT);
if (!$id) { // If no id
    include 'page-not-found.php'; // Page not found
}

$sql = "SELECT forename, surname 
        FROM member 
        WHERE id = :id;"; // SQL query
$statement = $pdo->prepare($sql); // Prepare
$statement->execute([':id' => $id]); // Execute
$member    = $statement->fetch(); // Get data

if (!$member) { // If no data
    include 'page-not-found.php'; // Page not found
}
?>

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Query strings and prepared statements</title>
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


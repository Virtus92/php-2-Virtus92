# Function to Execute SQL Statements
Getting PDO to run a SOL query and return the result set requires two or three statements, writing a user-defined function lets you do it in one.

When a SQL query does not use parameters, the PDO object's query() method will run a SQL query and return a PDOStatement object representing the result set:
```php
$statement = $pdo->query($sql);
```
When a SQL query does use parameters, the PDO object's prepare() method must be called to create a PDOStatement object that represents the query. Then the PDOStatement object's **execute()** must be called to run the query.
```php
$statement = $pdo->prepare($sql);
$statement->execute($sql);
```
After these steps, one of the PDOStatement object's methods must collect the data from the result set.
```php
function pdo(PDO $pdo, string $sql, array $arguments = null){
    if (!$arguments) { // If no arguments
        return $pdo->query($sql); // Run SQL and return PDOStatement object
    }
    $statement = $pdo->prepare($sql); // If arguments prepare statement
    $statement->execute($arguments); // Execute statement
    return $statement; // Return PDOStatement object
}
```

The function below has three parameters:
- $pdo is for the PDO object used to manage the connection to the database
- $sql is for the SQL query that is to be run
- $arguments is an array of SQL parameter names and their replacement values, note the default value if this argument is not provided is null

The function checks if no arguments were supplied:
- If not, it will run the query() method and the PDOStatement object that has been generated.
- If provided, it will call the prepare() method to create a PDOStatement object, call that objects execute() method to run the query, then return the PDOStatement object.

**When the user-defined pdo () function is called, method chaining is used to run the query and return the data in a single statement.**

When a PDOStatement object has been created and the SQL statement has been run, one of the following three methods is called to get the data from the result set and store it in a variable:
- **fetch()** gets a single row of data
- **fetchAll()** gets multiple rows of data
- **fetchColumn()** gets a value from a single column

When a function or method returns an object, **method chaining** lets you call a method of the object that is returned in the same statement.

Below, when the pdo() function is called, it will return a PDOStatement object. The function call is followed by an object operator, and a call to a method of the PDOStatement object that it returned.

```php
$members = pdo($pdo, $sql)->fetchAll();
$member = pdo($pdo, $sql, $arguments)->fetch();
```
When providing arguments for the PDOStatement object's execute() method, you can provide an associative array where the keys match the names of the parameters in the SQL statement (as shown already), or you can provide an indexed array where the values are in the same order that the placeholders appear in the SQL statement.

## Example without parameters
```php
$sql = "SELECT forename, surnameFROM member;";
$members = pdo($pdo, $sql)->fetchAll();
```
## Example with parameters
```php
$sql = "SELECT forename, surname FROM member WHERE id = :id;";
$member = pdo($pdo, $sql, ['id' => $id])->fetch();
```
<a href="http://blog.vjeux.com/2009/php/mysqli-wrapper-short-and-secure-queries.html">MysqliWrapper</a> - Short and Secure Queries
===============

Mysqli Wrapper is shortening the code required to run queries, make them 100% safe against SQL Injections and gives a handy Array as result. No more pain writing queries!

When developing a PHP application, SQL queries is the most dangerous area. This is because the built-in tools are either not secure by conception or too much complicated to use. I've made a little wrapper to mysqli that solves all these problems and make you enjoy writing queries!

What's good about this:

* A single 6 characters function
* Secure because parameterized
* Returns an Array
* Easy migration from the basic method


Example
-------

```javascript
$db = new dbWrapper('host', 'user', 'pass', 'database', true);
$db->handle()->set_charset('utf8mb4');

//data type of the column:
// s = string
// i = integer
// d = double
// b = blob

$result = $db->q('
  SELECT Name, CountryCode
  FROM City WHERE Zip = ? AND Population > ?',
  'si', $zip, $pop);

foreach ($result as $key => $city) {
  // $city['Name'], $city['CountryCode']
}

$result = $db->q('
  UPDATE City
  SET Population = ?
  WHERE Zip = ?',
   'is', $pop, $zip);
// $result = number of affected rows

$result = $db->q('
  DELETE FROM City
  WHERE Zip = ?',
  's', $zip);
// $result = number of deleted rows

$result = $db->q('
  INSERT INTO City (Zip, Population)
  VALUES (?, ?);',
  'si', $zip, $pop);
// $result = 1 in case of success

```

Read the full explanation on my blog: http://blog.vjeux.com/2009/php/mysqli-wrapper-short-and-secure-queries.html

<!-- 
.. title: PHP: Use an array value inside a here document
.. slug: php-use-an-array-value-inside-a-here-document
.. date: 03/28/2014 00:00:00 AM UTC+02:00
.. tags: web, php
.. link: 
.. description: 
.. type: text
-->

Just enclose your `$user['name']` with curly brackets.

Example:

```php
<?php
echo <<<END
Hello, my name is {$user['name']} and I live in {$user['country']}.
Today's date is $date.
END;
?>
```

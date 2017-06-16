### You (or Joomla) is likely including this file multiple times. Enclose your function in a conditional block:
```php
if (!function_exists('parseDate')) {
    // ... proceed to declare your function
}
```

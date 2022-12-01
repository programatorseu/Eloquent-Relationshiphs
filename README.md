<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>


for debugging inside `tinker`
give me db facade - with query and bindings : ]


```bash
DB::listen(function($sql){var_dump($sql->sql, $sql->bindings); });
```
or  so we listen for sql quer and we dumped the
```php
DB::enableQueryLog();
$user = User::first();
DB::getQueryLog();
```
result we got :
```
 [
     [
       "query" => "select * from `users` limit 1",
       "bindings" => [],
       "time" => 5.98,
     ],
   ]
```
   
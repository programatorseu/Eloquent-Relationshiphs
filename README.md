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
   

   run in tinker
   we do not need to specify namespace path in Tinker session any more 

   ```bash
   Post::factory()->create()
   Post::factory()->create(['user_id'=>2]);

   User::find(2)->posts
   ```

   ```bash
   $post = Post::find(1);
   $post->tags->pluck('name');
   ```
   with many to many we have : 
   1. pivot table `post_tag`
   2. `@tags` method -> belongsTo(Tags) called from Post
   3. `@posts` method -> belongsTo(Tags) called from Tag

install laravel debug bar 

### Has-Many-Through
Create Affiliation mfc
run few factories

- add affiliation_id collumn to users migration 
  
```sql
 select id from users where affiliation_id = 1; # 5,6
 select * from posts where user_id in (5,6)
```
inside Affiliation `@posts` method : 
```php
    return $this->hasManyThrough(Post::class, User::class);
```


Tinker session
```
$sport = Affiliation::whereName('sport')->first();
$sport->posts;
```

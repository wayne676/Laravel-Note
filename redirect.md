### web.php
```php
Route::match(['get', 'post'], '/user/dashboard', 'DashboardController@home')->name('dashboard');
```
### controller.php
```php
return redirect()->route('dashboard',['DisplayPanel=mana-list']);
```

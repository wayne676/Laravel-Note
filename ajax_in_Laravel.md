### web.php
```php
Route::post('/ajax/profileAjaxSave','ajax\dashboardAjaxController@profileStore');
```
need pay attention to the controller path:
```
'ajax\dashboardAjaxController@profileStore'
```

### xxx.js
```php
function editInformation(show) {

    var bio =  $('[name=user-bio]').val();
    var phone = $('[name=user-phone]').val();
    
    var postData = {
         bio: bio,
         phone: phone,
     };
     
    $.ajaxSetup({
      headers: {
          'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
      }
	  });
    
    $.ajax({
        url:"/ajax/profileAjaxSave", 
        data: postData, //{phone:phone}
        type:'post', 
        error: function (jqXHR, textStatus, errorThrown) {
            console.log("error", errorThrown, jqXHR, textStatus.responseText);
        },
        success: function (response, text, jqxhr) {
            console.log(response);
        }
    }); 
    return true; 
}
```
Attention
Route and ajax url path must be same, and defalut directory is under views:
```php
'/ajax/profileAjaxSave'
```
One more thing! Do not forget:
```php
$.ajaxSetup({
		headers: {
		    'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
		}
	});
```
Also you need add :
```php
 <meta name="csrf-token" content="{{ csrf_token() }}" />
```
in you head part

### dashboardAjaxController.php
This file I created in the ajax directory that is under the controller directory
```php
namespace App\Http\Controllers\ajax;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;

class dashboardAjaxController extends Controller
{
	function __construct()
    {
        $this->middleware('auth');
        parent::__construct();
    }
    public function profileStore(Request $request){
    	$user = Auth::user();
    	$user->phone=$request->input('phone');
    	$user->save();
    	return "saved";
	}
}
```
namespace and imported class need to be careful. especially for:
```php
namespace App\Http\Controllers\ajax;

use App\Http\Controllers\Controller;
```

### profileAjaxSave.php 
In terms of the profileAjaxSave file, you do not need edit it. 

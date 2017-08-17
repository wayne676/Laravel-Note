### form ajax传输
```html
<form action="" id="request_project" method="post">
  // your code here
</form>
```

jquery:
```javascript
$("#request_project").submit(function(event){
        event.preventDefault();
        console.log("prevent");
        var postData = $("#request_project").serialize();
        console.log(postData);
        $.ajaxSetup({
          headers: {
              'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
          }
          });
        $.ajax({
            url: "/ajax/placeOrder",
            data: postData,
            type: 'post',
            error: function (jqxhr, errorthrown, status) {
                console.log(jqxhr, errorthrown, status);
                showAlert("Could not decline bid.", 'error');
            },
            success: function (data, jqxhr) {
                console.log(data);
                data = JSON.parse(data);
                if (data["status"]) {
                    console.log(123213);
                    alert(data["what"], 'success');
                }
                else {
                    showAlert(data["message"], 'error');
                }
            }
        });
    });
```
$("#request_project").serialize();传入的数据request->all() 工作正常

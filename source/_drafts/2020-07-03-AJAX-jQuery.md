---
title: AJAX-jQuery
date: 2020-07-03 14:00:53
categories: AJAX
tags: 
- AJAX
- jQuery
---
之前使用 jQuery 上的 ajax 一直無法順利抓到值
因為預設是非同步 async: true
改成 async: false 就可以只是官網說用太多使用者體驗不好不太建異(頁面會假死)
<!--more-->
總之就是使用 promise 並用 ```.then``` 接後續動作 (類似下面程式碼)
後來大家又覺得寫太多就使用 promise 的 await 來簡化 promise 的流程。

但前端一直在快速發展後來出現 fetch 、 axios 都是為了更簡便達到一樣的效果。

```
function ajaxDeleteProduct() {
    
    // 這邊是要填的資訊.需要依照情況更改
    const ajaxUrl = '{{route('name')}}';
    const data = {
        id: 999,
        "_token": "{{csrf_token()}}",
        "_method": "post",
    };
    const method = 'DELETE';


    const ajaxMasterDefer = ajaxMaster(ajaxUrl, data, method);

    $.when(ajaxMasterDefer).then(
        // resolve 成功
        function (response) {
            
        },
        // reject 失敗
        function (response) {
            console.log('ajaxDeleteProduct() response error')
        },
        // pending loading 可以用 loading 效果
        function (response) {
        }
    );
}

//  jQuery ajax
function ajaxMaster(ajaxUrl, data, method) {
    const ajaxDefer = $.Deferred(); //取得認證
    $.ajax({
        url: ajaxUrl,
        method: method,
        data: data,
        success: function (response) {
            ajaxDefer.resolve(response);
        },
        error: function (response) {
            ajaxDefer.reject(response);
        }
    });
    return ajaxDefer.promise();
}
```
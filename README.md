## 日常工作中的一些js语句可以直接引用进来的

### JS判断移动设备最佳方法 并实现跳转至手机版网页
    <script type=”text/javascript”>
        if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) {
        window.location = “mobile.html”; //可以换成http地址
        }
    </script>
</hr>
### jquery ajax 函数
    $.ajax({
    type: 'POST',
    url: url,
    data: data,
    dataType: dataType,
    success: function() {},
    error: function() {}
    })

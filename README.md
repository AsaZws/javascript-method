## 日常工作中的一些js语句可以直接引用进来的

### JS判断移动设备最佳方法 并实现跳转至手机版网页
    <script type=”text/javascript”>
        if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) {
        window.location = “mobile.html”; //可以换成http地址
        }
    </script>

### jquery ajax 函数
    $.ajax({
    type: 'POST',
    url: url,
    data: data,
    dataType: dataType,
    success: function() {},
    error: function() {}
    })
    
### axios 
    可以在node.js中使用
    提供了并发请求的接口
    支持Promise API
    
    axios({
    method: 'GET',
    url: url,
    })
    .then(res => {console.log(res)})
    .catch(err => {console.log(err)})

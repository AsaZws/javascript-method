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
    
    并发请求
    function getUserAccount() {
      return axios.get('/user/12345');
    }

    function getUserPermissions() {
      return axios.get('/user/12345/permissions');
    }

    axios.all([getUserAccount(), getUserPermissions()])
      .then(axios.spread(function (acct, perms) {
        // Both requests are now complete
      }));
      
### JS判断移动设备最佳方法 并实现跳转至手机版网页
##### html =>
    <div id="wrap" class="wrap">
		<div id="top" class="top"></div>
		<div id="bottom" class="bottom"></div>
	</div>
	<div style="height: 2000px;width: 100%;"></div>
##### css =>
    *{
			margin: 0;
			padding: 0;
		}
		.wrap{
			width: 100%;
			height: 300px;
			position: relative;
		}
		.wrap .top{
			width: 80%;
			margin: 0 auto;
			height: 250px;
			background-color: #FF9999;
		}
		.wrap .bottom{
			width: 80%;
			margin: 0 auto;
			height: 50px;
			background-color: #2323A0;
		}
		.wrap .fix{
			position: fixed;
			top: 0;
			left: 10%;
		}
##### js =>
    var wrap,tops,bottom;
	window.onload=function(){
		wrap=document.getElementById("wrap")
		tops=document.getElementById("top");
		bottom=document.getElementById("bottom");
		document.onscroll=function(){
			var scroll=document.body.scrollTop||document.documentElement.scrollTop;
			if(scroll>=tops.offsetHeight){
				bottom.classList.add("fix");
			}
			else{
				bottom.classList.remove("fix");
			}
		}
	}

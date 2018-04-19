## 日常工作中的一些js语句可以直接引用进来的

### 1.JS判断移动设备最佳方法 并实现跳转至手机版网页
    <script type=”text/javascript”>
        if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) {
        window.location = “mobile.html”; //可以换成http地址
        }
    </script>
    
### 2.jquery ajax 函数
    $.ajax({
    type: 'POST',
    url: url,
    data: data,
    dataType: dataType,
    success: function() {},
    error: function() {}
    })
    
### 3.axios 
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
      
### 4.网页滑动头部固定
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
### 倒计时
#### html =>
	<input type="button" value="请阅读此协议(10)" disabled=disabled id="btn"/>
#### js =>
	//设置setInterval事件，1秒跳转一次
    //设置一个变量来记录每一秒的变化
    //找到按钮	
	var btn = document.getElementById("btn");
    //记录倒计时
	var num = 10;
	var timeID=setInterval(function () {
        //按钮上的文字
		btn.value = '请阅读此协议('+num+')';
        //每一秒少一个数字
		num--;
        //当倒计时结束之后，按钮上变为“我同意”,停止倒计时
		if(num == 0){
            //按钮上的子发生变化
			btn.value="我同意";
            //按钮可以点击
			btn.disabled=false;
            //清除倒计时
			clearInterval(timeID);
		}
	},1000);//间隔1秒一次

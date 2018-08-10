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
### 5.倒计时
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
### 6.方块动态图
#### html =>
	<div class="container">
			<ul class="boxList">
				<li></li>
				<li></li>
				<li></li>
				<li></li>
				<li></li>
				<li></li>
				<li></li>
				<li></li>
				<li></li>
			</ul>
		</div>
#### css =>
	*{margin: 0; padding: 0;}
			ul,li{list-style: none;}
			.container{perspective: 1300;-webkit-perspective:1300;}
			.boxList{position:absolute;width: 630px;height:630px;left:50%;margin-left:-315px; -webkit-transform-style: preserve-3d;transform-style: preserve-3d;/*animation: a1 2s 1;*/transition: all 2s;}
			.boxList li{float: left;width: 200px;height: 200px;margin:5px;background: darkcyan;-webkit-transition: all 0.3s;transition: all 0.3s;}
			.on li:hover{-webkit-transform: translate3d(0,0,30px);transform: translate3d(0,0,30px);background:deepskyblue;box-shadow: 30px 30px 10px rgba(0, 0, 0, 0.5);}
			.on{webkit-transform: rotateX(75deg) rotateY(0deg) rotateZ(45deg);transform: rotateX(75deg) rotateY(0deg) rotateZ(45deg);}
#### js =>
	var list=document.querySelector('.boxList');
		window.onload=function(){
			setInterval(transition,1000)
			
		}
		function transition(){
			list.className='on boxList';
		}
### 7.密码强度检测
	<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<title>密码强度检测</title>
	<style type="text/css">
	body{font:12px/1.5 Arial;}
	input{float:left;font-size:12px;width:150px;font-family:arial;border:1px solid #ccc;padding:3px;}
	input.correct{border:1px solid green;}
	input.error{border:1px solid red;}
	#tips{float:left;margin:2px 0 0 20px;}
	#tips span{float:left;width:50px;height:20px;color:#fff;overflow:hidden;background:#ccc;margin-right:2px;line-height:20px;text-	align:center;}
	#tips.s1 .active{background:#f30;}
	#tips.s2 .active{background:#fc0;}
	#tips.s3 .active{background:#cc0;}
	#tips.s4 .active{background:#090;}
	</style>
	<script type="text/javascript">
	window.onload = function ()
	{
	 var oTips = document.getElementById("tips");
 	var oInput = document.getElementsByTagName("input")[0];
 	var aSpan = oTips.getElementsByTagName("span");
	 var aStr = ["弱", "中", "强", "非常好"];
	 var i = 0; 
 
	 oInput.onkeyup = oInput.onfocus = oInput.onblur = function ()
	 {
  	var index = checkStrong(this.value);
  	this.className = index ? "correct" : "error";
  	oTips.className = "s" + index;
  	for (i = 0; i < aSpan.length; i++)aSpan[i].className = aSpan[i].innerHTML = "";
  	index && (aSpan[index - 1].className = "active", aSpan[index - 1].innerHTML = aStr[index - 1])
	 }
	};
	/** 强度规则
 	+ ------------------------------------------------------- +
 	1) 任何少于6个字符的组合，弱；任何字符数的同类字符组合，弱；
 	2) 任何字符数的两类字符组合，中；
 	3) 12位字符数以下的三类或四类字符组合，强；
 	4) 12位字符数以上的三类或四类字符组合，非常好。
 	+ ------------------------------------------------------- +
	**/
	//检测密码强度
	function checkStrong(sValue)
	{
 	var modes = 0;
 	if (sValue.length < 6) return modes;
 	if (/\d/.test(sValue)) modes++; //数字
 	if (/[a-z]/.test(sValue)) modes++; //小写
 	if (/[A-Z]/.test(sValue)) modes++; //大写  
 	if (/\W/.test(sValue)) modes++; //特殊字符
 	switch (modes)
 	{
 	 case 1:
  	 return 1;
  	 break;
  	case 2:
  	 return 2;
  	case 3:
 	 case 4:
  	 return sValue.length < 12 ? 3 : 4
   	break;
 	}
	}
	</script>
	</head>
	<body>
	<input type="password" value="" maxlength="16" />
	<div id="tips"><span></span><span></span><span></span><span></span></div>
	</body>
	</html>
### 8.显示屏居中
	遮罩层：
	    width: 100%;
	    height: 100%;
	    position: fixed;
	    left: 0;
	    top: 0;
	    background: rgba(0,0,0,0.6);
	    z-index: 100;
	显示层：
	    width: 100%;
	    height: 500px;
	    background: url(box_bg.png) no-repeat;
	    background-size: cover;
	    position: fixed;
	    top: 50%;
	    left: 50%;
	    -moz-transform: translate(-50%, -50%);
	    -ms-transform: translate(-50%, -50%);
	    -webkit-transform: translate(-50%, -50%);
	    transform: translate(-50%, -50%);
	    z-index: 200;
### 9.JS实现键盘监听(包括组合键)
       document.onkeydown=function(event){ 
            var e = event || window.event || arguments.callee.caller.arguments[0]; 
            if(e && e.keyCode==27){ // 按 Esc  
                //要做的事情 
				alert("按 esc"); 
            } 
            if(e && e.keyCode==113){ // 按 F2  
                //要做的事情 
				alert("按 f2"); 
            }             
            if(e && e.keyCode==13){ // enter 键 
                //要做的事情 
				alert("按 Enter"); 
            }
			if (e.keyCode == 86 && e.ctrlKey) {  
                alert("你按下了ctrl+V");  
            }
         }; 

# 通过本地存储localstorage存储图片的代码

```
	var src="demo.jpg";

	function set(key){
		var img=document.createElement('img');
	
		img.addEventListener("load",function(){
			//创建一个canvas
			var imgCanvas=document.createElement("canvas"),
			imgContext=imgCanvas.getContext("2d");
			//确保canvas元素的大小和图片的尺寸一致
			imgCanvas.width=this.width;
			imgCanvas.height=this.height;
			//渲染图片到canvas中,使用canvas的drawImage()方法
			imgContext.drawImage(this,0,0,this.width,this.height);
			//用canvas的dataUrl的形式取出图片,imgAsDataURL是一个base64的字符串
			var imgAsDataURL=imgCanvas.toDataURL("image/png");
			//保存到本地存储中
			//使用try-catch()查看是否支持localstorage
			try{
				localStorage.setItem(key,imgAsDataURL);//将取出的图片存放到localStorage 
			}
			catch(e) {
			 console.log("Storage failed:"+e);//存储失败
			}
			
		},false);
		img.src=src;
	}	
	function get(key) {//从本地缓存获取图片并且渲染
	var srcStr=localStorage.getItem(key);//从localStorage中取出图片
	var imgObj=document.createElement('img');//创建一个img标签
	imgObj.src=srcStr;
	document.body.appendChild(imgObj);
	}
	
		注释：
		(1)、这个比较适合用在不常更改的图片，但是如果图片的base64大小比较大的话，将比较耗费localStorage的资源；
		
		(2)、canvas有一个安全策略的问题：如果图片和你本身请求的域名不在同一个域名下，浏览器会报出一个安全问题，这个时候我们要给我们的服务器加一个“允许跨域”访问的响应头————Access Orign=*,这样来保证你的图片可进行跨域被canvas来画；

```

# loaclstorage 控制过期时间
```
function set(key,y){
	var curTime=new Date().getTime();
	//存储一个当时存储时候的时间
	localStorage.setItem(key,JSON.stringify({data:v,time:curTime}));

}
function get(key,exp) {
	var data=localStorage.getItem(key);
	var dataObj=JSON.parse(data);
	if(new Date().getTime()-dataObj.time>exp) {//get出来的时间减去当时存储的时间大于过期时间，那么就认为过期
	   console.log("过期");
	}else {
	//否则，返回值
	 console.log("data="+dataObj.data);
	}
}

```

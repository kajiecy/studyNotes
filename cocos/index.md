# Cocos Creator 开发笔记

- 使对象沿某一轴旋转
``` js
    let dici;
    dici.is3DNode = true;
    dici.eulerAngles = cc.v3(0, 180, 0) // cc.cv(x,y,z);
```
- 监听用户触屏事件
``` js
    this.node.on(cc.Node.EventType.TOUCH_START,(e)=>{
        //世界坐标
        let touchPoint = e.getLocation(); // touchPoint = {x,y}
    },this)
```
- 插入预制资源
```js
   let dici = cc.instantiate(this.dici);
   this.node.addChild(dici);
```
- 碰撞检测

1. 给不同的对象建立分组
2. 在分组中编辑碰撞规则
3. 在main.js 中开始碰撞检测
4. 在挂载对象的js中添加碰撞触发逻辑
```js
    let manager = cc.director.getCollisionManager();
    manager.enabled = true; // 开启碰撞
    manager.enabledDebugDraw = true; // 调试状态绘制出我们物体的碰撞器的形状
```

```
    // 碰撞开始事件(第一次接触)
    onCollisionEnter: function (other, self) {
        console.log("other.name = ", other.node.name, other.node.group, other.node.groupIndex);
    }
    // 碰撞持续事件(组件相交)
    onCollisionStay: function (other, self) {
        console.log("other.name = ", other.node.name, other.node.group, other.node.groupIndex);
    }
    // 碰撞结束事件(离开的一瞬间)
    onCollisionExit: function (other, self) {
        console.log("other.name = ", other.node.name, other.node.group, other.node.groupIndex);
    }
```
- 开始一个定时器
``` js
    this.schedule(()=>{
        console.log('开始倒计时');
    },1)
```
- 场景跳转
```js
    cc.director.loadScene('场景名称')
```
- 播放音乐

不要用AudioSource(太坑了,浪费我两小时)!!播放音乐就用cc.audioEngine.playMusic();
```
        
        bgAudio:{
            default:null,
            type:cc.AudioClip,
        },
        cc.audioEngine.playMusic(this.bgAudio,true); // 播放背景音乐
        cc.audioEngine.playEffect(this.bgAudio,false); // 播放音效
        cc.audioEngine.setEffectsVolume(.2); //音效大小
```

- 修改载入界面

先执行构建 替换splash.XXXXX.png (背景图片)
修改css  style-mobile.XXXXX.css、style-desktop.XXXXX.css 中 
```css
#splash {
  background: #171717 url(./splash.85cfd.png) no-repeat fixed;
  background-size: 100% 100%;
}
```
将背景图片平铺

自定义进度条底部
```css
.progress-bar {
    position: absolute;
    left: 10%;
    top: 47%;
    height: 28px;
    padding: 4px;
    width: 80%;
    border-radius: 50px;
    /* box-shadow: 0 1px 5px #000 inset, 0 1px 0 #444; */
    background-color: #110936;
}
.progress-bar span{
    border-radius: 50px;
    overflow: hidden;
}
#progress-number{
    width: 28px;
    height: 28px;
    display: inline-block;
    font-size: 12px;
    line-height: 28px;
    background: white;
    opacity: .68;
    color: #3dc5de;
    float: right;
}

```
html中加入 
```html
<div class="progress-bar stripes">
  <span style="width: 0%">
    <!--加入span-->
    <span id="progress-number">0%</span>
  </span>
</div>
```
main.js 中加入 
```js
    function setLoadingDisplay () {
        // 此处省略部分代码
        var progressNumber = document.getElementById('progress-number');
        cc.loader.onProgress = function (completedCount, totalCount, item) {
            // 此处省略部分代码
            if (progressBar) {
                // 此处省略部分代码
                progressNumber.innerHTML = percent.toFixed(0) + '%';
            }
        };
        // 此处省略部分代码
    }
```
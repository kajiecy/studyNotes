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

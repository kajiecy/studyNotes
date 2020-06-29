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
```js
    let manager = cc.director.getCollisionManager();
    manager.enabled = true; // 开启碰撞
    manager.enabledDebugDraw = true; // 调试状态绘制出我们物体的碰撞器的形状
```
4. 在挂载对象的js中添加碰撞触发逻辑
```js
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
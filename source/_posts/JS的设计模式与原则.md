title: Javascript 中的设计模式与原则
date: 2019-07-22 18:43:28
tags:
author:
---
#### Javascript 中的设计模式与原则
1. 何为设计？
   + 即按照哪一种思路或者标准来实现功能
   + 功能相同，可以有不同设计方案来实现
   + 伴随着需求增加，设计的作用才能体现出来
2. 结合《UNIX/LINUX设计哲学》中设计的准则
   + 准则1：小即是美
   + 准则2：让每个程序只做好一件事
   + 准则3：快速建立原型
   + 准则4：舍弃高效率而取可移植性
   + 准则5：采用纯文本来存储数据
   + 准则6：充分利用软件的杠杆效应（软件复用）
   + 准则7：使用 shell 脚本来提高杠杆效应和可移植性
   + 准则8：避免强制性的用户界面
   + 准则9：让每个程序都称为过滤器
   + 小准则：允许用户定制环境
   + 小准则：尽量使操作系统内核小而轻量化
   + 小准则：使用小写字母并尽量简短
   + 小准则：沉默是金（输入错误，不要输出）
   + 小准则：各部分之和大于整体
   + 小准则：寻求 90% 的解决方案
    <!--more--> 
3. SOLID 五大设计原则
  + S-单一职责原则
     + 一个程序只做好一件事
     + 如果功能过于复杂就拆分开，每个部分保持独立
  + O-开放封闭原则
     + 对扩展开放，对修改封闭
     + 增加需求时，扩展新代码，而非修改已有代码
     + 这是软件设计的终极目标
  + L-李氏置换原则
     + 子类能覆盖父类
     + 所有父类出现的地方，子类就能出现
     + JS中使用较少（弱类型 & 继承使用较少）
  + I-接口独立原则
     + 保持接口的单一独立，避免出现"胖接口"
     + JS中没有接口（typescript例外），使用较少
     + 类似于单一职责原则，这里更关注接口
  + D-依赖倒置原则
    + 面向接口编程，依赖于抽象而不依赖于具体
    + 使用方只关注接口而不关注具体类的实现
    + JS中使用较少（没有接口 & 弱类型）
4. 设计模式（设计原则和模版，从"设计到模式"）
  + 创建型
     + [工厂模式（工厂方法模式、抽象工厂模式、建造者模式ps：在 Java 中这些具体的工厂模式是需要分开讲的，所以这里只有21种设计模式）](#Factory_Pattern)
     + [单例模式](#Singleton_Pattern)
     + [原型模式](#Prototype_Pattern)
  + 组合型/结构型
    + [适配器模式](#Adapter_Pattern)
    + [装饰器模式](#Decorator_Pattern)
    + [代理模式](#Proxy_Pattern)
    + [外观模式](#Facade_Pattern)
    + [桥接模式](#Bridge_Pattern)
    + [组合模式](#Composite_Pattern)
    + [享元模式](#Flyweight_Pattern)
  + 行为型
    + [策略模式](#Strategy_Pattern)
    + [模版方法模式](#Template_Method_Pattern)
    + [观察者模式](Observer_Pattern)
    + [迭代器模式](Iterator_Pattern)
    + [职责链模式](Chain_of_Responsibility_Pattern)
    + [命令模式](Command_Pattern)
    + [备忘录模式](Memento_Pattern)
    + [状态模式](State_Pattern)
    + [访问者模式](Visitor_Pattern)
    + [中介者模式](Mediator_Pattern)
    + [解释器模式](Interpreter_Pattern)
    
###### 1.工厂模式 (Factory) 👇<span id="Factory_Pattern"> </span>
+ 介绍
  + 将 new 操作单独封装
  + 遇到 new 时，就要考虑是否该使用工厂模式
+ 示例
  + 你去购买汉堡，直接点餐、取餐，不会自己亲手做
  + 商店要“封装”做汉堡的工作，做好直接给买者
+ UML类图
    ![upload successful](/images/pasted-180.png)
+ 代码

 ```javascript
class Product {
    constructor(name) {
        this.name = name
    }
    init() {
        alert('init')
    }
    fun1() {
        alert('fun1')
    }
    fun2() {
        alert('fn2')
    }
}
class Creator {
    creator(name) {
        return new Product(name)
    }
}
//测试
let creator = new Creator()
let p = creator.creator('p1')
p.init()
p.fun1()
   ```
+ 使用场景
   + jQuery - $('div')
 ```javascript
class jQuery {
    constructor(selector) {
        let slice = Array.prototype.slice
        let dom = slice.call(document.querySelectorAll(selector))
        let len = dom ? dom.length : 0
        for (let i = 0; i < len; i++) {
            this[i] = dom[i]
        }
        this.length = len
        this.selector = selector || ''
    }
    append(node) {

    }
    addClass(name) {

    }
    html(data) {

    }
    // 此处省略若干 API
}
window.$ = function (selector) {
    return new jQuery(selector)
}
  ```
   + React.createElement  
   React里的JSX其实就是语法糖,这是它的语法
    ![upload successful](/images/pasted-181.png)
   编译之后的代码为：
    ![upload successful](/images/pasted-182.png)
    
    ![upload successful](/images/pasted-183.png)
    也是工厂模式
   + Vue 异步组件
    ![upload successful](/images/pasted-184.png)
+ 设计原则验证
   + 构造函数和创建者分离
   + 符合开放封闭原则

###### 2.单例模式 (Singleton) 👇<span id="Singleton_Pattern"> </span>
+ 介绍
  + 系统中被唯一使用
  + 一个类只有一个实例
+ 示例
  + 登陆框，一个系统只有一个
  + 购物车，一个商城也只有一个
+ UML类图  
Java 中的UML类图
![Java 中的UML类图](/images/pasted-186.png "Java 中的UML类图")
+ 代码
   + 说明
      + 单例模式需要用到 Java 的特性 （ private ）
      + ES6 中没有 （ typescript 除外 ）
      + 只能用 java 代码来演示 UML 图的内容
   + Java 中的
   ```java
   public class SingletonObject {
    //注意，私有化构造函数，外部不能 new ，只能内部能 new
    private SingletonObject(){
    }
    //唯一被 new 出来的对象
    private static SingletonObject instance = null;
    //获取对象的唯一接口
    public static SingletonObject getInstance(){
        if(instance == null){
            // 只 new 一次
            instance = new SingletonObject();
        }
        return instance;
    }
   //对象方法
    public void showMessage(){
    }
}
```
测试
 ```java
 public class SingletonPatternDemo {
    public static void main (String[] args) {
        //不合法的构造函数
        //编译时错误：构造函数 SingletonObject() 是不可见 的！！！
        //SingletonObject object = new  SingletonObject();

        //获取唯一可用的对象
        SingletonObject object = SingletonObject.getInstance();
    }
}
```
   +  JavaScript中的
```javascript
class SingleObject {
    login() {
        console.log('login...')
    }
}
//挂在类上，是静态函数
SingleObject.getInstance = (function () {
    let instance
    return function () {
        if(!instance) {
            instance = new SingleObject();
        }
        return instance
    }
})()
let obj1 = SingleObject.getInstance()
obj1.login()
let obj2 = SingleObject.getInstance()
obj2.login()
console.log('obj1 === obj2',obj1 === obj2)
console.log('---分割线---')
let obj3 = new SingleObject()
obj3.login()
console.log('obj1 === obj3',obj1 === obj3)
```
   控制台打印  
![upload successful](\images\pasted-188.png)
+ 使用场景
   + jQuery 只有一个 $
   ![upload successful](\images\pasted-190.png)
   + vuex 和 redux 中的 store
   + 模拟登陆框/购物车
```javascript
   class LoginForm{
    constructor() {
        this.state = 'hide'
    }
    show(){
        if(this.state === 'show'){
            alert('已经显示')
            return
        }
        this.state = 'show'
        console.log('登录框显示成功')
    }
    hide() {
        if(this.state === 'hide') {
            alert('已经隐藏')
            return
        }
        this.state = 'hide'
        console.log('登陆框隐藏成功')
    }
}
LoginForm.getInstance = (function(){
    let instance
    return function () {
        if(!instance){
            instance = new LoginForm()
        }
        return instance
    }
})()
//测试
let login1 = LoginForm.getInstance()
login1.show()
let login2 = LoginForm.getInstance()
login2.hide()
console.log('login1 === login2',login1 === login2)
```
   控制台输出
   
![upload successful](\images\pasted-191.png)

+ 设计原则验证
   + 符合单一职责原则，只实例化唯一对象
   + 没法具体开放封闭原则，但是绝对不违反开放封闭原则

###### 3.原型模式 (Prototype) 👇<span id="Prototype_Pattern"> </span>
+ 介绍
+ 示例
+ UML类图
+ 代码
+ 使用场景
+ 设计原则验证
###### 4.适配器模式 (Adapter) 👇<span id="Adapter_Pattern"> </span>
+ 介绍
  + 就接口格式和使用者不兼容
  + 中间加一个适配转换接口
+ 示例
  + 电源转换头
+ UML类图
![upload successful](/images\pasted-192.png)
+ 代码
```javascript
class Adaptee {
    specificRequest() {
        return '德国标准插头'
    }
}
class Target{
    constructor() {
        this.adaptee = new Adaptee()
    }
    request() {
        let info = this.adaptee.specificRequest()
        return `${info} - 转换器 - 中国标准插头`
    }
}
//测试
let target = new Target()
let res = target.request()
console.log(res)
```
   控制台输出
![upload successful](/images/pasted-193.png)
+ 使用场景
   + Vue 的 computed
   + 封装旧接口
![upload successful](/images/pasted-194.png)  
![upload successful](/images/pasted-196.png)
    
+ 设计原则验证
  + 将旧接口和使用者分离，符合开放封闭原则

###### 5.装饰器模式 (Decorator) 👇<span id="Decorator_Pattern"> </span>
+ 介绍
  + 为对象添加新功能
  + 不改变其原有的结构和功能
+ 示例
  + 手机壳，不影响手机本身的使用
+ UML类图
Java 中的UML类图 
  ![upload successful](/images/pasted-197.png) 
  Javascript 中的UML类图  
![upload successful](/images/pasted-198.png)
+ 代码
```javascript
class Circle {
    draw() {
        console.log('画一个圆形')
    }
}
class Decorator {
    constructor(circle) {
        this.circle = circle
    }
    draw() {
        this.circle.draw()
        this.setRedBorder(circle)
    }
    setRedBorder(circle) {
        console.log('设置红色边框')
    }
}
//测试代码
let circle = new Circle()
circle.draw()
console.log('---分隔线---')
let dec = new Decorator(circle)
dec.draw()
```
控制台输出
![upload successful](/images/pasted-199.png)
+ 使用场景
   + ES7 装饰器
   + core-decorators
###### 6.代理模式 (Proxy) 👇<span id="Proxy_Pattern"> </span>
+ 介绍
   + 使用者无权访问目标对象
   + 中间加代理，通过代理做授权和控制
+ 示例
   + 科学上网
   + 明显经纪人
+ UML类图  
Java 中的UML类图 
  ![upload successful](/images/pasted-200.png)
Javascript 中的UML类图 
![upload successful](/images/pasted-201.png)
+ 代码
```javascript
class ReadImg{
    constructor(filename) {
        this.fileName = filename
        this.loadFromDisk()
    }
    display(){
        console.log('dispaly...' + this.fileName)
    }
    loadFromDisk(){
        console.log('loading...' + this.fileName)
    }
}
class ProxyImg{
    constructor(fileName) {
        this.realImg = new ReadImg(fileName)
    }
    display(){
        this.realImg.display()
    }
}
//test
let proxyImg = new ProxyImg('1.png')
proxyImg.display()
```
控制台输出
![upload successful](/images/pasted-202.png)
+ 使用场景
    + 网页事件代理
    + jQuery $.proxy
    + ES6 Proxy
###### 7.外观模式 (Facade) 👇<span id="Facade_Pattern"> </span>
+ 介绍
  + 为子系统中的一组接口提供了一个高层接口
  + 使用者使用这个高层接口
+ 示例
![upload successful](/images/pasted-203.png)
去医院看病，接待员去挂号、门诊、划价、取药
+ UML类图
![upload successful](/images/pasted-204.png)
+ 使用场景
![upload successful](/images/pasted-205.png)
事件绑定
+ 设计原则验证
   + 不符合单一职责原则和开放封闭原则，因此谨慎使用，不可滥用（胖接口）
 
###### 8.桥接模式 (Bridge) 👇<span id="Bridge_Pattern"> </span>
###### 9.组合模式 (Composite) 👇<span id="Composite_Pattern"> </span>
###### 10.享元模式 (Flyweight) 👇<span id="Flyweight_Pattern"> </span>
###### 11.策略模式 (Strategy) 👇<span id="Strategy_Pattern"> </span>
###### 12.模版方法模式 (Template Method) 👇<span id="Template_Method_Pattern"> </span>
###### 13.观察者模式 (Observer) 👇<span id="Observer_Pattern"> </span>
+ 介绍
   + 发布&订阅
   + 一对多
+ 示例
   + 点咖啡，点好之后坐等被叫
+ UML类图
Java 中的UML类图 
![upload successful](/images/pasted-206.png)
Javascript 中的UML类图 
![upload successful](/images/pasted-207.png)
+ 代码
```javascript
// 主题，接收状态变化，触发每个观察者
class Subject {
    constructor() {
        this.state = 0
        this.observers = []
    }
    getState() {
        return this.state
    }
    setState(state) {
        this.state = state
        this.notifyAllObservers()
    }
    attach(observer) {
        this.observers.push(observer)
    }
    notifyAllObservers() {
        this.observers.forEach(observer => {
            observer.update()
        })
    }
}
// 观察者，等待被触发
class Observer {
    constructor(name, subject) {
        this.name = name
        this.subject = subject
        this.subject.attach(this)
    }
    update() {
        console.log(`${this.name} update, state: ${this.subject.getState()}`)
    }
}
// 测试代码
let s = new Subject()
let o1 = new Observer('o1', s)
let o2 = new Observer('o2', s)
let o3 = new Observer('o3', s)
s.setState(1)
s.setState(2)
s.setState(3)
```
+ 使用场景
+ 设计原则验证
###### 14.迭代器模式 (Iterator) 👇<span id="Iterator_Pattern"> </span>
###### 15.职责链模式 (Chain of Responsibility) 👇
<span id="Chain_of_Responsibility_Pattern"> </span>

###### 16.命令模式 (Command) 👇
<span id="Command_Pattern"> </span>

###### 17.备忘录模式 (Memento) 👇<span id="Memento_Pattern"> </span>

###### 18.状态模式 (State) 👇<span id="State_Pattern"> </span>

###### 19.访问者模式 (Visitor) 👇<span id="Visitor_Pattern"> </span>

###### 20.中介者模式 (Mediator) 👇<span id="Mediator_Pattern"> </span>

###### 21.解释器模式 (Interpreter) 👇<span id="Interpreter_Pattern"> </span>

参考资料：  
1. [ 23 种设计模式用英语如何表达？](https://blog.csdn.net/john_f_lau/article/details/40558963)
2. [Javascript 设计模式系统讲解与应用](https://coding.imooc.com/class/255.html)
3.
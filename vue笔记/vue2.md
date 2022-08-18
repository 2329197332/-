# 1.Vue的简介
## 1.1 Vue官网
+ [中文官网](https://cn.vuejs.org/)
## 1.2 介绍与描述
+ Vue是一套用来动态构建用户界面的渐进式JavaScript框架
  + 构建用户界面：把数据通过某种办法变成用户界面
  + 渐进式：Vue可与自底向上逐层的应用，简单应用只需要一个轻量小巧的核心库，复杂应用可与引入各式各样的Vue插件
+ 作者：尤雨溪
  
![](https://img-blog.csdnimg.cn/img_convert/12442ea33447259058415aafd172de1b.png)

## 1.3 Vue的特点
1. 遵循MVVM模式
2. 编码简介，体积小，运行效率高，适合移动端/PC端开发
3. 它本身只关注UI，可与引入其他第三方库开发项目
4. 采用`组件化`模式，提高代买复用率、且让代码更好维护

![](https://img-blog.csdnimg.cn/img_convert/1d42eb2118634bfb5563ef0b74aabb1a.png)

5. `声明式`编码。让编码人员无需直接操作DOM，提高开发效率

![](https://img-blog.csdnimg.cn/img_convert/f5b9fa1a6e14a801a3f6d23c5c364cac.png)

6. 使用`虚拟DOM`和`Diff`算法，尽量复用DOM节点

![alt](https://img-blog.csdnimg.cn/img_convert/694b0c4236fbfb179d53fa1a953069a8.png)

## 1.4 与其他JS框架的关联
+ 借鉴angulatr的**模板**和**数据绑定**技术
+ 借鉴react的**组件化**和**虚拟DOM**技术
## 1.5 Vue 周边库
+ vue-cli：vue脚手架
+ vue-router：路由
+ vuex：状态管理（他是vue的插件但是没有用vue-xxx的命名规则）
+ vue-lazyload：图片懒加载
+ vue-scroller：页面滑动相关
+ mint-ui：基于vue得到UI组件库（移动端）
+ element-ui：基于vue的UI组件库（PC端）
# 2.初始Vue
## 2.1 前置工作
1. 给浏览器按照[Vue Devtools](https://github.com/vuejs/vue-devtools)插件
2. 标签引入Vue包
3. （可选）阻止vue在祁东式生成生产提示Vue.config.productionTip = false
4. favicon需要将页签图标放在项目跟径，重新打开就有了（shift+F5强制刷新）
## 2.2 初识Vue
1. 想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象
2. root 容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法
3. root 容器里的代码被称为Vue模板
4. Vue 实例与容器是一一`对应`的
5. 真实开发中只有一个Vue实例，并且会配合着组件一起使用
6. `{{xxx}}`中的 xxx 要写`js表达式`，且 xxx 可以自动读取到data中的所有属性  
**注意区分**：js 表达式 和 js代码（语句）  
7. 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方  
a=a+b   
demo(1) x === y ? ‘a’ : ‘b’
8. js代码（语句）if(){} for(){}
9. 一旦data中的数据发生变化，那么模板中用到该数据的地方也会自动更新(Vue实现的响应式)
``` html
<!-- 引入Vue -->
<script type="text/javascript" src="../js/vue.js"></script>
<!-- 准备好一个容器 -->
<div id="demo">
	<h1>Hello，{{name.toUpperCase()}}，{{address}}</h1>
</div>
<script type="text/javascript" >
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
	//创建Vue实例
	new Vue({
		el:'#demo', //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。
		data:{ //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象。
			name:'hello,world',
			address:'北京'
		}
	});
</script>
```
# 3.模板语法 数据绑定 #
## 3.1 模板语法
`Vue`模板语法有2大类
+ **插值语法**
  + 功能：用于解析标签体内容
  + 写法：`{{xxx}}`,xxx是**js表达式**，且可以直接读取到data中的所属性
+ **指令语法**
  + 功能：用于解析标签（包括：标签属性、标签体内容、绑定事件...）
  + 举例：`v-bind:href="xxx"`或简写为`:href="xxx"`，xxx同样要写`js表达式`，且可以直接读取到data中的所属性
  + 备注：Vue中有很多的指令，且形式都是**v-xxx**,此处只是拿`v-bing`举例
``` html
<div id="root">
  <h2>插值语法</h2>
  <h4>你好，{{ name }}</h4>
  <hr />
  <h2>指令语法</h2>
  <a v-bind:href="tencent.url.toUpperCase()" x="hello">点我去看{{ tencent.name }}1</a>
  <a :href="tencent.url" x="hello">点我去看{{ tencent.name }}2</a>
</div>
<script type="text/javascript">
  new Vue({
    el: '#root',
    data: {
      name: 'jack',
      tencent: {
        name: '开端',
        url: 'https://v.qq.com/x/cover/mzc00200mp8vo9b/n0041aa087e.html',
      }
    }
  })
</script>
```
![](https://img-blog.csdnimg.cn/img_convert/6a6c4b05b135275c79b10d3a48d1b809.png)

## 3.2数据绑定
Vue中有2种数据绑定的方式”
+ 单项绑定`（v-bind）`：数据只能从data流向页面
+ 双向绑定`（v-model）`：数据不仅能从data流向页面，还可以从页面流向data
>  注意  
>双向绑定一般都应用在**表单类元素**上（如：input、select等）  
>v-model:value可以简写为`v-model`，因为v-model默认收集的就是value值

``` html
<div id="root">
	<!-- 普通写法 单向数据绑定 -->
    单向数据绑定：<input type="text" v-bind:value="name"><br/>
    双向数据绑定：<input type="text" v-model:value="name"><br/>
    
    <!-- 简写 v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值-->
    单向数据绑定：<input type="text" :value="name"><br/>
    双向数据绑定：<input type="text" v-model="name"><br/>
    
    <!-- 如下代码是错误的，因为 v-model 只能应用在表单类元素（输入类元素）上 -->
	<!-- <h2 v-model:x="name">你好啊</h2> -->
</div>
<script>
  new Vue({
		el:'#root',
		data:{
			name:'jack',
    }
	})
</script>
```
# 4.el和data的两种写法
## 4.1 el的两种写法
+ 创建Vue实例对象的时候配置el属性
+ 先创建Vue实例，随后再通过vm.$mount('#root')指定el的值
``` javascript
const v = new Vue({
  //第一种写法
  el:'#root', 
  data: {
    name:'dselegent'
  }
})
console.log(v)
```
``` javascript
//第二种写法
v.$mount('#root') 
```
## 4.2 data的两种写法
``` javascript
//对象式
data:{
  name:"张三"
}
```
``` javascript
//函数式
data(){
  return{
    name:"张三"
  }
}
```
+ **如何选择**：目前哪种写法都可以，以后到组件时，data必须使用函数式，否则会报错
+ **重要原则**：由Vue管理的函数，一定不要写箭头函数，否则this就不再是Vue实例了

# 5.MVVM模型
![](https://img-blog.csdnimg.cn/img_convert/35f3f59320c9984409388b0ffe8244ec.png)
## 5.1 MVVM模型
+ M：模型`Model`，data中的数据
+ V：视图`View`，模板代码
+ VM：视图模型ViewModel，Vue实例（相当于数据和页面的连接桥梁）
## 5.2 观察发现
+ `data`中的所有属性，最后都出现在了`vm`身生
+ vm身生所有的属性及Vue原型身上所有的属性，在Vue模板中都可以直接使用
``` html
<div id="root">
  <h2>名称：{{ name }}</h2>
  <h2>战队：{{ team }}</h2>
  <h2>测试：{{ $options }}</h2>
</div>
<script>
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: { 
      name: 'uzi',
      team: 'RNG'
    }
  })
</script>
```
# 6.数据代理
了解数据代理需要js的一些知识：`Object.defineProperty()`，属性表只，属性描述符，`getter`,`setter`...
## 6.1 数据代理简介
建议学习文章地址：  
[https://zh.javascript.info/property-descriptors](https://zh.javascript.info/property-descriptors)  
[https://zh.javascript.info/property-accessors](https://zh.javascript.info/property-accessors)  
这里简单介绍一下  
**属性标志**  
对象属性（`properties`），除`value`外，还有三个特殊的特性（`attribus`），也就是所谓的"标志"
+ `writable` —— 如果为`true`，则值可以被修改，否则它只是可读的
+ `enumerable` —— 如果为`true`，则表示是可以遍历的，可以在`for...in Object.keys()`中遍历出来
+ `configurab` —— 如果为`true`，则此控制属性可以被删除，默认值是`false`  

**Object.defineProperty**(`obj` , `prop` , `descriptor`)
>obj：要定义属性的对象  
>prop：要定义或修改的属性的名称  
>descriptor：要定义或修改的属性描述符号
``` javascript
let number = 18
let person = {
  name: '张三',
  sex: '男',
}

Object.defineProperty(person, 'age', {
  // value:18,
  // enumerable:true,		// 控制属性是否可以枚举，默认值是false
  // writable:true,			// 控制属性是否可以被修改，默认值是false
  // configurable:true	// 控制属性是否可以被删除，默认值是false

  // 当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
  get() {
    console.log('有人读取age属性了')
    return number
  },

  // 当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
  set(value) {
    console.log('有人修改了age属性，且值是', value)
    number = value
  }

})
// console.log(Object.keys(person))
console.log(person)
```
## 6.2 Vue中的数据代理
**数据代理：** 通过一个对象代理另一个对象中的属性的操作（读/写）
``` javascript
let vm = {};
let data = {
  name: 'ds',
  age: 18,
};
Object.defineProperty(vm, 'age', {
  get() {
    return data.age;
  },
  set(value) {
    data.age = value;
  },
});
```
![](https://img-blog.csdnimg.cn/img_convert/08184766cc308e64719b2238f661bf9b.png)
>使用{{}}插值语法获取vm的x时，触发get方法，将data的x赋值给vm的x  
>修改data中的age时并没有改变vm里的age的值，当{{}}获取vm中age的值时，就会将data的age赋值给vm的age  
>修改vm中的age，触发set方法，将修改的值赋值给data中的age

1. Vue中的数据代理通过vm对象代理`data`对象中属性的操作（读/写）
2. Vue中数据代理的好处：更加方便的操作`data`中的数据
3. 基本原理
   + 通过`object.defineProperty()`把`data`对象中所有属性添加到`vm`上
   + 为每一个添加到`vm`上的属性，都指定一个`getter`，`setter`
   + 在`getter`，`setter`内部去操作（读/写）`data`中对应的属性

![](https://img-blog.csdnimg.cn/img_convert/877aba6679cd1a3be2fcccd37efba9a0.png)

>`Vue`将`data`中的数据拷贝了一份到`_data`属性中，又将`_data`里面的属性提取到`Vue`实例中（如`name`），通过`definePropertys()`实现数据代理，这样通过`getter/setter`操作`name`，进而操作`_data`中的`name`。而`_data`又对`data`进行数据劫持，实现响应式  

>`name`被修改-调用`setter`->重新解析模板->生成新的虚拟`DOM`->新旧`DOM`对比（`diff`）->更新页面

# 7.事件处理
## 7.1 事件的基本用法
1. 使用`v-on:xxx`或`@xxx`绑定事件，其中xxx是事件名
2. 事件的回调需要配置在`methods`对象中，最终会在`vm`上
3. `methods`中配置的函数，不要用箭头函数，否则指向就部署`vm`了
4. `methods`中配置的函数，都是被`Vue`所管理的函数，`this`的指向是`vm`或组件实例对象
5. `@click="demo"`和`@click="demo($event)"`效果一致，。但后者可以传参  

``` html
<!-- 准备好一个容器-->
<div id="root">
  <h2>欢迎来到{{name}}学习</h2>
  <!-- <button v-on:click="showInfo">点我提示信息</button> -->
  <button @click="showInfo1">点我提示信息1（不传参）</button>
  <!-- 主动传事件本身 -->
  <button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
</div>
<script>
	const vm = new Vue({
    el:'#root',
    data:{
      name:'vue',
    },
    methods:{
      // 如果vue模板没有写event，会自动传 event 给函数
      showInfo1(event){
        // console.log(event.target.innerText)
        // console.log(this) //此处的this是vm
        alert('同学你好！')
      },
      showInfo2(event,number){
        console.log(event,number)
        // console.log(event.target.innerText)
        // console.log(this) //此处的this是vm
        alert('同学你好！！')
      }
    }
	});
</script>
```
## 7.2 事件修饰符
`Vue`中的事件修饰符
1. `preven` 阻止默认事件（常用）
2. `stop` 阻止事件冒泡（常用）
3. `once` 事件只触发一次（常用）
4. `capture` 使用事件的捕获模式
5. `self` 只有`event.target`是当前操作的元素时才触发事件
6. `passive` 事件的默认行为立即执行，无需等待事件回调执行完毕
>修饰符可以连续写，比如可以这么用`@click.prevent.stop="showInfo`"
``` html
<style>
  * {margin-top: 20px;}
  .demo1 {height: 50px;background-color: skyblue;}
  .box1 {padding: 5px;background-color: skyblue;}
  .box2 {padding: 5px;background-color: white;}
  .list {width: 200px;height: 200px;background-color: skyblue;overflow: auto;}
  li {height: 100px;}
</style>
<div id="root">
  <h2>欢迎来到{{ name }}学习</h2>
  
  <!-- 阻止默认事件（常用） -->
  <a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>
  
  <!-- 阻止事件冒泡（常用） -->
  <div class="demo1" @click="showInfo">
    <button @click.stop="showInfo">点我提示信息</button>
    <!-- 修饰符可以连续写 -->
    <!-- <a href="http://www.qq.com" @click.prevent.stop="showInfo">点我提示</a> -->
  </div>
  
  <!-- 事件只触发一次（常用） -->
  <button @click.once="showInfo">点我提示信息</button>
   
  <!-- 使用事件的捕获模式 -->
  <div class="box1" @click.capture="showMsg(1)">捕获到的时候就直接触发
div1
    <div class="box2" @click="showMsg(2)">div2</div>
  </div>
   
  <!-- 只有event.target是当前操作的元素时才触发事件； -->
  <div class="demo1" @click.self="showInfo">
    <button @click="showInfo">点我提示信息</button>
  </div>
  
  <!-- 事件的默认行为立即执行，无需等待事件回调执行完毕； -->
  <!-- scroll是滚动条滚动，passsive没有影响 -->
  <!-- wheel是鼠标滚轮滚动，passive有影响 -->
  <ul @wheel.passive="demo" class="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
  </ul>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      name: '尚硅谷'
    },
    methods: {
      showInfo(e) {
        alert('同学你好！')
        // console.log(e.target)
      },
      showMsg(msg) {
        console.log(msg)
      },
      demo() {
        for (let i = 0; i < 100000; i++) {
          console.log('#')
        }
        console.log('累坏了')
      }
    }
  })
</script>
```
## 7.3 键盘事件
>键盘上的每个按键都有自建的名称和编码，例如：Enter（13）。而Vue还对一些常用按键起了别名方便使用
1. `Vue`中常用的按键别名  
   + 回车 `Enter`
   + 删除 `delete` 捕获“删除和退格键”
   + 退出 `esc`
   + 空格 `space`
   + 换行 `tab` 特殊，必须配合`keydown`去使用
   + 上 `up`
   + 下 `down`
   + 左 `left`
   + 右 `right`
2. `Vue`未提供别名的按键，可以使用按键原始的`key`值去绑定，但要注意转化为`kebab-case`（多单词小写短横线写法 `Numlock(num-lock)` `Capslock(caps-lock)`）
3. 系统修饰符（用法特殊）`ctrl`、`alt`、`shift`、`meta`（`meta`就是`win`键）
   + 配合`keyup`使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才触发
   + 配合`keydown`使用：正常触发事件
4. 也可以使用`keyCode`去指定具体的按键 **（不推荐）**  
`@keyup.13 = xxx(@keyup.enter = xxx)`
5. Vue.config.keyCodes 自定义键名 = 键码
``` html
<div id="root">
  <h2>欢迎打开{{name}}笔记</h2>
  <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo"><br/>
  <input type="text" placeholder="按下tab提示输入" @keydown.tab="showInfo"><br/>
  <input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo"><br/>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false	// 阻止 vue 在启动时生成生产提示。
  Vue.config.keyCodes.huiche = 13		// 定义了一个别名按键
  new Vue({
    el: '#root',
    data: {
      name: 'vue'
    },
    methods: {
      showInfo(e) {
        // console.log(e.key,e.keyCode)
        console.log(e.target.value)
      }
    },
  })
</script>
```

# 8.计算属性
## 8.1 插值语法实现
``` html
<title>姓名案例_methods实现</title>
<div id="root">
  姓：<input type="text" v-model="firstName"><br/>
  名：<input type="text" v-model="lastName"><br/>
  全名：<span>{{ fullName() }}</span>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      firstName: '张',
      lastName: '三'
    },
    methods: {
      fullName() {
        return this.firstName + '-' + this.lastName
      }
    },
  })
</script>
```
![](https://img-blog.csdnimg.cn/img_convert/90d63b19c51b96f191d9c5f723bbf54c.png)
## 8.2 methods实现
>数据发生变化，模板就会重新解析  

``` html
<title>姓名案例_methods实现</title>
<div id="root">
  姓：<input type="text" v-model="firstName"><br/>
  名：<input type="text" v-model="lastName"><br/>
  全名：<span>{{ fullName() }}</span>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      firstName: '张',
      lastName: '三'
    },
    methods: {
      fullName() {
        return this.firstName + '-' + this.lastName
      }
    },
  })
</script>
```
## 8.3 computed实现
+ 定义：要用的属性不存在，要通过已有属性计算得来
+ 原理：底层借助了Objcet.defineProperty方法提供的getter和setter
+ get函数什么时候执行？
  + 初次读取时会执行一次
  + 当依赖的数据发生变化时会被再次调用
+ 优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便
+ 备注：
  + 计算属性最终也会出现在vm上，直接读取使用即可
  + 如果计算属性要被修改，那就必须写set函数去相应修改，且set要引起计算时依赖的数据发生变化
  + 如果计算属性确定不考虑修改，可以使用计算属性的简写形式
>以下完整写法
``` html
<!-- 准备好一个容器-->
<div id="root">
  姓：<input type="text" v-model="firstName">
  名：<input type="text" v-model="lastName"> 
  全名：<span>{{fullName}}</span>
</div>
<script>
	const vm = new Vue({
    el:'#root',
    data:{
      firstName:'张',
      lastName:'三',
    }
    computed:{
      fullName:{
        //get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
        //get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
        get(){
          console.log('get被调用了')
            return this.firstName + '-' + this.lastName
        },
        //set什么时候调用? 当fullName被修改时。
        // 可以主动在控制台修改fullName来查看情况
        set(value){
          console.log('set',value)
          const arr = value.split('-')
          this.firstName = arr[0]
          this.lastName = arr[1]
        }
      }
    }
  })
</script>
```
![](https://img-blog.csdnimg.cn/img_convert/f5a899c1831edc1c472110b782eda760.png)
![](https://img-blog.csdnimg.cn/img_convert/f5a899c1831edc1c472110b782eda760.png)
>以下简写形式  
``` html
<!-- 准备好一个容器-->
<!-- 准备好一个容器-->
<div id="root">
    姓：<input type="text" v-model="firstName">
    名：<input type="text" v-model="lastName"> 
    全名：<span>{{fullName}}</span>
</div>
<script>
	const vm = new Vue({
    el:'#root',
    data:{
      firstName:'张',
      lastName:'三',
    }
    computed:{
      fullName() {
        console.log('get被调用了')
			  return this.firstName + '-' + this.lastName
    	}
    }
  })
</script>

```
>读取fullName时会自动调用get方法

## 8.4 method和computed区别
``` html
<title>姓名案例_methods实现</title>
<div id="root">
  姓：<input type="text" v-model="firstName"><br/>
  名：<input type="text" v-model="lastName"><br/>
  全名：<span>{{ fullName() }}</span>
  全名：<span>{{ fullName() }}</span>
  全名：<span>{{ fullName() }}</span>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      firstName: '张',
      lastName: '三'
    },
    methods: {
      fullName() {
        return this.firstName + '-' + this.lastName
      }
    },
  })
</script>
```
>如果只使用一次，其实没什么区别
>使用多次的时候，method每次都会重新调用，而computed会从缓存中读取
# 9.监听属性
## 9.1 methods实现
``` html
<div id="root">
  <h3>今天天气很{{ info }}</h3>
  <!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句 -->
  <!-- <button @click="isHot = !isHot">切换天气</button> -->
  <button @click="changeWeather">切换天气</button>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el:'#root',
    data:{
      isHot:true,
    },
    computed:{
      info(){
        return this.isHot ? '炎热' : '凉爽'
      }
    },
    methods: {
      changeWeather(){
        this.isHot = !this.isHot
      }
    }
  })
</script>

```
![](https://img-blog.csdnimg.cn/img_convert/b054b71621dab5a6f6f6f05e6bc46915.png)
## 9.2 watch实现
监视属性`watch`：
+ 当监视的属性发生变化时，回调函数自动调用，进行相关操作
+ 监视的属性必须存在，才能进行监视，既可以监视`data`，也可以监视计算属性
+ 配置项属性`immediate:false`，改为`true`，则初始化时调用一次
+ 监视的两种写法：
  + `new Vue`时传入`watch`配置
  + 通过`vm.$watch`监视
>第一种写法

``` html 
<!-- 准备好一个容器-->
<div id="root">
    <h2>今天天气很{{ info }}</h2>
    <button @click="changeWeather">切换天气</button>
</div>
<script>
	const vm = new Vue({
    el:'#root',
    data:{
      isHot:true,
    },
    computed:{
      info(){
        return this.isHot ? '炎热' : '凉爽'
      }
    },
    methods: {
      changeWeather(){
        this.isHot = !this.isHot
      }
    },
    watch:{
      isHot:{
        immediate: true, // 初始化时让handler调用一下
        // handler什么时候调用？当isHot发生改变时。
        handler(newValue, oldValue){
          console.log('isHot被修改了',newValue,oldValue)
        }
      }
    } 
  })
</script>
```
>第二种写法
``` html
<!-- 准备好一个容器-->
<div id="root">
    <h2>今天天气很{{ info }}</h2>
    <button @click="changeWeather">切换天气</button>
</div>
<script>
	const vm = new Vue({
    el:'#root',
    data:{
      isHot:true,
    },
    computed:{
      info(){
        return this.isHot ? '炎热' : '凉爽'
      }
    },
    methods: {
      changeWeather(){
        this.isHot = !this.isHot
      }
    }
  }) 
  vm.$watch('isHot',{
    immediate:true, //初始化时让handler调用一下
    //handler什么时候调用？当isHot发生改变时。
    handler(newValue,oldValue){
      console.log('isHot被修改了',newValue,oldValue)
    }
  })
</script>
```
## 9.3 深度监视
+ Vue中的`watch`默认不监视对象内部值的改变（一层）`obj:{name:'ds',age:18}`这里的一层指的是后面整个对象的字面量，而不是里面的值是第一层
+ 配置`deep:true`可以监测对象内部值的改变（多层）
>备注  
>1. `Vue`自身可以监测 对象内部值的改变，但是`Vue`提供的`watch`默认不可以
>2. 使用`watch`时根据数据的具体结构，决定是否采用深度监视
``` html
<div id="root">
  <h3>a的值是:{{ numbers.a }}</h3>
  <button @click="numbers.a++">点我让a+1</button>
  <h3>b的值是:{{ numbers.b }}</h3>
  <button @click="numbers.b++">点我让b+1</button>
  <button @click="numbers = {a:666,b:888}">彻底替换掉numbers</button>
  {{numbers.c.d.e}}
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el: '#root',
    data: {
      isHot: true,
      numbers: {
        a: 1,
        b: 1,
        c: {
          d: {
            e: 100
          }
        }
      }
    },
    watch: {
      // 监视多级结构中某个属性的变化
      /* 'numbers.a':{
				handler(){
					console.log('a被改变了')
				}
			} */
      // 监视多级结构中所有属性的变化
      numbers: {
        deep: true,
        handler() {
          console.log('numbers改变了')
        }
      }
    }
  })
</script>
```
![](https://img-blog.csdnimg.cn/img_convert/87d1cf803e81f967919bd3730796aa44.png)
## 9.4 简写
如果监视属性除了`handler`没有其他配置的话，可以进行简写
``` html
<div id="root">
  <h3>今天天气很{{ info }}</h3>
  <button @click="changeWeather">切换天气</button>
</div>
<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el: '#root',
    data: {isHot: true,},
    computed: {info() {return this.isHot ? '炎热' : '凉爽'}},
    methods: {changeWeather() {this.isHot = !this.isHot}},
    watch: {
      //简写
      isHot(newValue, oldValue) {
        console.log('isHot被修改了', newValue, oldValue)
      }
    }
  })
  //简写
  // vm.$watch('isHot', (newValue, oldValue) => {
  // 	console.log('isHot被修改了', newValue, oldValue, this)
  // })
</script>
```
>监视到`isHot`改变会自动调用`handler`方法

## 9.5 computed和watch之间的区别
+ computed能完成的功能，watch都可以完成
+ watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作
>两个重要原则  
>1. 被Vue所管理的函数，最好写成普通函数，这样this的指向才是vm或者组件实例对象
> 2. 所有不被Vue所管理的函数（定时器的回调函数，ajax的回调函数等、Promise的回调函数），最好写成箭头函数，这样this的指向才是vm或者组件实例对象
比如想延迟一秒显示fullName只能用watch实现
``` javascript
new Vue({
  el:'#root',
  data:{
    firstName:'张',
    lastName:'三',
    fullName:'张-三'
  },
  watch:{
    firstName(val){
      setTimeout(()=>{
        this.fullName = val + '-' + this.lastName
      },1000);
    },
    lastName(val){
      this.fullName = this.firstName + '-' + val
    }
  }
})
```
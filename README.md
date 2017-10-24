# Vue-directive
指令分成五类

***

### 第一类文本类

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>文本操作类</title>
    <script src="node_modules/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <!--{{}} 文本插值-->
    <p>{{message}}1</p>
    <!--v-text 赋值给textContent-->
    <p v-text="message">1</p>
    <!--v-html 展示html代码-->
    <p v-html="html"></p>
    <!--v-bind :缩写 单向数据绑定 属性绑定-->
    <p :id="box"></p>
    <!--v-model 双向数据绑定-->
    <input type="text" v-model="username">
</div>
<script>
    new Vue({
        el:'#app',
        data:{
            message:'Hello,Vue.js',
            html:`<h1>我是一段HTML</h1>`,
            username:'我是一个input标签'
        }
    })
</script>
</body>
</html>
```

***

### 第二类事件类

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>事件操作类</title>
    <script src="node_modules/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <!--v-on 绑定监听事件-->
    <div v-on:click="clicked">我是一个点击事件</div>
    <!--@简写   修饰符 取消默认事件prevent 取消冒泡stop once只调用一次(例如点赞)-->
    <!--支持所有原生标签事件-->
    <div @click.prevent.stop="clicked">我是一个取消冒泡和默认事件的点击事件</div>
    <!--v-on:click="handle('ok', $event)" 支持简写-->
    <div @click="handle('ok',$event)">我是一个传参的点击事件</div>
    <!-- 键修饰符，键别名 -->
    <input @keyup.enter="onEnter">
    <!-- 键修饰符，键代码 -->
    <input ref="username" @keyup.13="onEnter">
    <!-- 点击回调只会触发一次 -->
    <button v-on:click.once="doThis">执行一次</button>
</div>
<script>
    new Vue({
        el:'#app',
        methods:{
            clicked:function () {
                console.log('我是一个点击事件')
            },
            handle:function (value) {
                console.log(value);
            },
            doThis:function () {
                console.log('只可以执行一次')
            },
            onEnter:function (event) {
                //执行完回车之后失去焦点
                event.target.blur();
                //操作其他input标签来获取焦点
                this.$refs.username.focus()
            }
        }
    })
</script>
</body>
</html>
```

***

### 第三类条件类

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>条件类</title>
    <script src="node_modules/vue/dist/vue.js"></script>
</head>
<body>


<div id="app">
    <!--v-if if判断 为false时不创建节点 为true时创建dom节点-->
    <p v-if="false">我是一段显示内容</p>
    <p v-if="isIf">我是一段显示内容</p>
    <!--v-else-if 表示 v-if 的 “else if 块”。可以链式调用。-->
    <div v-if="type === 'A'">
        A
    </div>
    <div v-else-if="type === 'B'">
        B
    </div>
    <div v-else-if="type === 'C'">
        C
    </div>
    <!--v-else-->
    <div v-else>
        Not A/B/C
    </div>
    <!--v-show 切换标签的 display 与if不同的是if是创建和移除节点操作,而show是切换css的display属性为none-->
    <p v-show="isShow">我是一段isShow</p>
    <button @click="clicked">按钮</button>
</div>
<script>
    new Vue({
        el:'#app',
        data:{
            type:'B',
            isIf:true,
            isShow:true
        },
        methods:{
            clicked:function () {
                this.isShow = !this.isShow;
                this.type = 'C';
                this.isIf = !this.isIf;
            }
        }
    })
</script>
</body>
</html>
```

***

### 循环类

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>循环类</title>
    <script src="node_modules/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <!--v-for 循环渲染 -->
    <!--此指令之值，必须使用特定语法 alias in expression-->
    <!--v-for可以获取到数组或json的index,value,key但是不能获取数组自身,还可以绑定key值唯一标识符-->
    <div v-for="(val, key, index) in array">{{val}}:{{key}}:{{index}}</div>
    <!--栗子:购物车或者列表排序-->
    <div v-for="item in array" :key="item.id">
        <a :href="item.url"> <img :title="item.title" :src="item.image" alt=""></a>

    </div>
</div>
</body>
<script>
    new Vue({
        el: '#app',
        data: {
            array: [{
                "title": "What You Need To Know About CSS Variables",
                "url": "http://tutorialzine.com/2016/03/what-you-need-to-know-about-css-variables/",
                "image": 'https://tutorialzine.com/media/2016/03/css-variables.jpg'
            },
                {
                    "title": "Freebie: 4 Great Looking Pricing Tables",
                    "url": "http://tutorialzine.com/2016/02/freebie-4-great-looking-pricing-tables/",
                    "image": 'https://tutorialzine.com/media/2016/02/great-looking-pricing-tables.jpg'
                },
                {
                    "title": "20 Interesting JavaScript and CSS Libraries for February 2016",
                    "url": "http://tutorialzine.com/2016/02/20-interesting-javascript-and-css-libraries-for-february-2016/",
                    "image": 'https://tutorialzine.com/media/2016/02/interesting-resources-february.jpg'
                },
                {
                    "title": "Quick Tip: The Easiest Way To Make Responsive Headers",
                    "url": "http://tutorialzine.com/2016/02/quick-tip-easiest-way-to-make-responsive-headers/",
                    "image": 'https://tutorialzine.com/media/2016/02/quick-tip-responsive-headers.png'
                },
                {
                    "title": "Learn SQL In 20 Minutes",
                    "url": "http://tutorialzine.com/2016/01/learn-sql-in-20-minutes/",
                    "image": 'https://tutorialzine.com/media/2016/01/learn-sql-20-minutes.png'
                },
                {
                    "title": "Creating Your First Desktop App With HTML, JS and Electron",
                    "url": "http://tutorialzine.com/2015/12/creating-your-first-desktop-app-with-html-js-and-electron/",
                    "image": 'https://tutorialzine.com/media/2015/12/creating-your-first-desktop-app-with-electron.png'
                }]
        }
    })
</script>
</html>
```

***

### 其他类

##### 包括v-pre v-once v-cloak

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>其他类</title>
    <style>
        [v-cloak]{
            display: none;
        }
    </style>
    <script src="node_modules/vue/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <!--v-pre 不需要写=号后面的内容 表示跳过此部分不进行编译,有利于优化-->
    <p v-pre>{{message}}</p>
    <!--v-once 不需要写=号后面的内容 表示只进行一次赋值 即使更改message也不会改变内容-->
    <p v-once>{{message}}</p>
    <!--v-cloak 不需要写=号后面的内容-->
    <!--使用css属性display来隐藏为编译完成之前的内容,这样就不会把编译的过程展现在界面上,
       适用于比较大的数据加载时使用-->
    <p v-cloak>{{message}}</p>
</div>
<script>
    new Vue({
        el:'#app',
        data:{
           message:'Hello Vue.js'
        }
    })
</script>
</body>
</html>
```

***


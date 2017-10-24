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


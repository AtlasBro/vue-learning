# 一.模板语法-插值-文本操作

### 1.v-once

表示锁定模板值

### 2.v-html

显示文本内容本身

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="vue3.js"></script>
</head>

<body>
    <div id='a'>
        <span v-once>
            {{get}}
        </span>
        <div>
            {{html}}
        </div>
        <div v-html="html">
        </div>
        <button v-on:click='a'>button</button>
    </div>
    
     <script>
         Vue.createApp({
             data:function(){
                 return{
                     content:"hello vue3",
                     abc:"abc",
                     num:0,
                     get:"一次",
                     html:"<div>123</div>"
                 }
             },
             methods:{
                 a:function(){
                     this.get = '10';//v-once锁死控件内容
                    //console.log(this);
                    //this.content='good';
                    //this.abc="lala";
                    //  var _this = this;
                    //  setInterval(function(){
                    //     _this.num++;
                    //  },1000);
                 },
                 b:function(){
                     alert(2);
                 }
             }
         }).mount("#a");

     </script>
</body>
</html>
```

若在使用v-html的控件内增加内容，内容会被覆盖

![image-20220207231605028](https://gitee.com/kawahara0616/typora-images/raw/master/202202072316117.png)

### 3.v-text

方法同上，不常用

### 4.总结

![image-20220207231735186](https://gitee.com/kawahara0616/typora-images/raw/master/202202072317278.png)

# 二.模板语法-插值-属性与表达式

### 1.v-bind

用于赋予属性

可以进行字符串拼接

也可进行三目运算符来改属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="vue3.js"></script>
    <style>
        span{transition: .3s;}
        .red{color:red}
        .blue{color:blue}
    </style>
</head>
<body>
    <div id="a">
        <span>{{name?content:color}}</span>
        
        <span v-html="name?span:div"></span>
        
        <span v-html="num==1?span:div"></span>        
        <span v-bind:abc="'blue'+ content">a</span>
        
        <span v-bind:class="name?'red':'blue'" v-on:click="change">sky</span>
        
        <button v-on:click='toRed'>red</button>
        
        <button v-on:click='toBlue'>blue</button>        
        {{content}}
        <span v-bind:class="color">123</span>
        
        <span v-bind:class="color" v-bind:id="'sky'">color</span> <!--若想将其变为字符串，需要一对单引号和一对双引号-->
    </div>
    <script>
        Vue.createApp({
            data:function(){
                return{
                    num:"1",
                    content:"123",
                    color:"red",
                    name:true,
                    span:"<span>span</span>",
                    div:"<div>div</div>"
                }
            },
            methods:{
                toRed:function(){
                    this.color='red';
                },
                toBlue:function(){
                    this.color='blue';
                },
                change:function(){
                    this.name = !this.name;//不断true false循环
                }
            }
        }).mount("#a");
    </script>
</body>
</html>
```

### 2.总结

![image-20220207235544050](https://gitee.com/kawahara0616/typora-images/raw/master/202202072355152.png)

# 三.模板语法-指令-动态参数

### 1.总结

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="vue3.js"></script>
    <style>
        .red{color:red}
        .blue{color:blue}
    </style>
</head>
<body>
    <div id="leo">
        <span v-on:[fn]="toRed" v-bind:class="color">123</span>
        <br/>
        <span v-bind:[sky]="content"></span> <!--中括号[]内可以放入key值-->
        <button v-on:click='change'>go!</button>
        <button v-on:click='toMouseOver'>mouseover</button>
    </div>
    <script>
        Vue.createApp({
            data:function(){
                return{
                    fn:"click",
                    color:"",
                    sky:"id",
                    content:"Vue3"
                }
            },
            methods:{
                change:function(){
                    this.sky="class";
                },
                toRed:function(){
                    if(this.color=="red"){
                        this.color="blue"
                    }
                    else{
                        this.color="red";
                    }
                },
                toMouseOver:function(){
                    this.fn="mouseover";
                }
            }
        }).mount("#leo");
    </script>
</body>
</html>
```



### ![image-20220211151558426](https://gitee.com/kawahara0616/typora-images/raw/master/202202111516703.png)

# 四.模板语法-缩写

### 1.总结

![image-20220211154051083](https://gitee.com/kawahara0616/typora-images/raw/master/202202111540196.png)

补充：

1.@mouseover就相当于v-on:mouseover，类似的方法同上

2.

![image-20220211153732926](https://gitee.com/kawahara0616/typora-images/raw/master/202202111537971.png)

![image-20220211153751218](https://gitee.com/kawahara0616/typora-images/raw/master/202202111537260.png)

以上写法相当于

```html
<span v-on:click="change" @mouseover="over">事件</span>
```

3.开发时使用缩写形式，增强可读性

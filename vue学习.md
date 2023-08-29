# vue学习

## vue定义

​	vue是一个用于**构建用户界面**的**渐进式** **框架**

创建vue实例，初始化渲染

1. 准备容器
2. 引入核心包
3. 创建vue实例new vue
4. 指定配置项:渲染数据
   1. el指定挂载点：数据管理区域
   2. data提供数据

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
    <div id="app">
        {{msg}}

    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            /* 管理数据区域 */
            el: '#app',
            /* 管理数据 */
            data: {
                msg: 'Hello Vue.js'
            }
        })
    </script>
</body>
</html>
```

## 插值表达式：只能够渲染需要被展示的内容。

​	{{表达式}}

​	表达式：可以被求值的代码

## vue核心特性：响应式(数据驱动视图)

## vue指令

vue根据不同的指令，针对不同的标签实现不同的功能。

带有v-前缀的的特殊属性。

- v-html 动态解析标签

- v-show display设置

  - v-show="表达式" true显示
  - 场景：频繁切换显示隐藏

- v-if 条件渲染

  - v-if="表达式" true显示 <u>底层设计是判断条件控制元素的创建和移除</u>
  - 场景：要么显示，要么隐藏不频繁切换的场景

- v-else

  - 紧跟v-if使用

- v-else-if

  - ```html
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>
        <div id="app">
            <p v-if="gender===1">男</p>
            <p v-else>女</p>
            <hr>
            <p v-if="score>=90">优秀</p>
            <p v-else-if="score>=70">良好</p>
            <p v-else-if="score>=60">及格</p>
            <p v-else>不及格</p>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            new Vue({
                /* 管理数据区域 */
                el: '#app',
                /* 管理数据 */
                data: {
                    gender:2,
                    score:60,
                }
            })
       </script>
    </body>
    </html>
    ```

- v-for

  - 基于数据循环，多次渲染整个元素-》数组对象数字4

  - v-for="(index,item) in list"

  - ```html
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>
        <div id="app">
            <button @click="index--" v-show="index>0">上一页</button>
           <img v-bind:src="list[index]" :title="msg" style="width: 500px;height: 300px;">
           <button @click="index++" v-show="index<list.length-1">下一页</button>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            var app = new Vue({
                el: '#app',
                data: {
                   index:0,
                   msg:"海景图片",
                   list:[
                    "./OIP-C.jpg",
                    "./OIP-C2.jpg",
                    "./R-C3.jpg"
                   ]
                }
            })
        </script>
    </body>
    </html>
    ```

  - v-for的默认行为会尝试原地修改元素

  - key:给元素添加唯一的标识便于vue进行列表项的正确排序复用

    - 值只能为字符串或者数字类型
    - 值必须唯一
    - 推荐使用id作为key

- v-on

  - 注册事件=添加监听+提供处理逻辑

  - v-on:事件名="内联语句"

  - v-on:事件名="methods中的函数名"

  - ```html
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>
        <div id="app">
            <div>
                <button v-on:click="count++">+</button>
                <span>{{count}}</span>
                <button @click="count--">-</button>
                
                <button @click="fn">显示与隐藏</button>
                <p v-show="isshow">hello world</p>
            </div>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            new Vue({
                /* 管理数据区域 */
                el: '#app',
                /* 管理数据 */
                data: {
                    count:0,
                    isshow: true
                }
                methods:{
                fn:function(){
                this.isshow=!this.isshow
            }
            }
            })
        </script>
    </body>
    </html>
    ```

  - 参数传递

    - ```html
      <!DOCTYPE html>
      <html>
      <head>
      </head>
      <body>
          <div id="app">
             <div class="box">
              <h3>小黑自动售票机</h3>
              <button @click="buy(5)">可乐五元</button>
              <button @click="buy(10)">咖啡十元</button>
             </div>
             <p>银行卡余额{{money}}元</p>
          </div>
          <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
          <script>
              var app = new Vue({
                  el: '#app',
                  data: {
                      money:999
                  },
                  methods: {
                      buy:function(a){
                          this.money-=a
                      }
                  }
              })
          </script>
      </body>
      </html>
      ```

- v-bind

  - 动态设置html标签属性src,title

  - v-bind:属性名="表达式"

  - ```html
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>
        <div id="app">
           <img v-bind:src="imgurl" :title="msg">
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            var app = new Vue({
                el: '#app',
                data: {
                   imgurl:"./OIP-C.jpg",
                   msg:"海景图片",
                }
            })
        </script>
    </body>
    </html>
    ```

  - ```html
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>
        <div id="app">
            <button @click="index--" v-show="index>0">上一页</button>
           <img v-bind:src="list[index]" :title="msg" style="width: 500px;height: 300px;">
           <button @click="index++" v-show="index<list.length-1">下一页</button>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            var app = new Vue({
                el: '#app',
                data: {
                   index:0,
                   msg:"海景图片",
                   list:[
                    "./OIP-C.jpg",
                    "./OIP-C2.jpg",
                    "./R-C3.jpg"
                   ]
                }
            })
        </script>
    </body>
    </html>
    ```

- v-model

  - 使用场景：表单

  - 双向绑定：快速获取或设置表单元素内容

  - ```html
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>
        <div id="app">
            <form action="#">
                用户名: <input type="text" v-model="info.user">
                <br>
                密 码:  <input type="password" v-model="info.pwd">
                <br>
                <button @click="reset">重置</button>
                <button @click="submit">提交</button>
            </form>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            var app = new Vue({
                el: '#app',
                data: {
                   info:{
                    user:"admin",
                    pwd:"123456",
                   }
                },
                methods:{
                    reset(){
                        this.info.user="",
                        this.info.pwd=""
                    },
                    submit(){
                        console.log(this.info.user,this.info.pwd);
                    }
                }
                
            })
        </script>
    </body>
    </html>
    ```

- v-slot

综合案例小黑记事本














































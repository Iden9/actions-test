---
title: "TypeScript使用简易流程"
date: 2024-10-03
---



TypeScript是什么呢？
TypeScript用来约束js在某些方面太动态了，比如变量没有类型。TS 以JS为基础构建的语言，TS扩展了JavaScript并添加了类型，TS不能被JS解析器直接执行，需要TS->编译->JS；

安装TypeScript 搭建TypeScript开发坏境
下载node.js
安装node.js
使用npm全局安装typescript 进入命令行npm i -g typescript安装成功：
image.png 4. 使用TS 新建.ts文件，然后需要编译为.js文件

image.png 在文件夹下面多出一个.js文件

image.png

TypeScript语法
1. 基本类型
对变量或者函数参数以及返回值都可以指定类型，有很多种类型，其中注意any unknown类型的区别，unknown是安全的any类型，不会影响别的变量； P4；

1. 对象属性指定
```ts
/*=========对象属性指定============*/
//对象b必须有name属性   属性后面？表示可选 没有其他没指定的属性
let b:{name:string,age?:number};
//表示对象除了指定的name 还有其他类型的属性都行
let c:{name:string,[propName:string]:any};
c={name:'猪八戒',age:13};
2. 函数结构指定
```
```ts
/*==========函数结构指定============*/
//指定函数相关 参数返回参数 即定义函数结构
let d:(a:number,b:number)=>number
3. 数组类型声明

/*=========数组类型声明============*/
//数组 string[]表示字符串数组
let e:string[];
e=['pink','a'];
let g:Array<number>;
g=[1,2,3];
4. 使用元组

/*
* 元组,元组就是固定长度的数组 
语法：[类型，类型，类型]长度为3
*/
let h:[string,string];
h=['hello','world']
4. enum枚举

/*==============enum枚举==============*/
// 把所有可能情况独列出来
enum Gender{
  Male=0,
  Female=1,
}
let i:{name:string,gender:Gender};
i={
  name:'随悟空',
  gender:Gender.Male
}
5. &

// &表示同时
let j:{name:string}&{age:number};
j={name:'孙悟空',age:13};
5. 类型别名

//类型别名
type myType=string;
type myType2=1|2|3|4;
let k:myType2;
let l:myType2;
let m:myType;
m='string';
```
以上的这些类型多写多用就记住了。

TypeScript的tsconfig.json配置文件
参考 tsc --init生成tsconfig.json配置文件，里面的属性分别什么意思使用到的时候自己查询；P9

TypeSCript的webpack打包使用
首先使用npm init -y初始化项目
下载一些包 npm i -D webpack webpack-cli typescript ts-loader,tsc --init
然后配置webpack.config.js文件，配置过程中遇到问题，webpack可能版本过高然后导致一些报错，比如在一些新的版本不需要手动设置入口文件，但是我去掉入口文件之后任然报错； 检擦发现文件路径有问题，src webpack.config.js不在part3文件夹下面一定要注意路径的正确性，
image.png 框里面的都是同一层的，然后在part3下面npm run build 自动生成html文件插件安装 npm i -D html-webpack-plugin在webpack.config.js中配置plugins
```js

 plugins: [
        new HTMLWebpackPlugin(),
    ]
```
再次运行npm run build可以在dist下面直接生成引用bundle.js的index.html文件，也可以在src下面提供一个index.html模板，在webpack.config.js下面配置;
```js
new HTMLWebpackPlugin({
            template: './src/index.html'
        }),
```
还需要下载自动刷新即热更新，安装：npm i -D webpack-dev-server 然后还是要在package.json文件里面配置

```json
"start": "webpack serve --open"
```
然后npm start,自动打开index.html文件，更新index.ts文件测试； 安装插件npm i -D clean-webpack-plugin 删除旧的dist目录，同样需要配置：

plugins: [
        new CleanWebpackPlugin(),
        ...
    ],
指定哪些文件允许作为模块引入：

resolve: {
        extensions: ['.ts', '.js']
    }
babel使用解决兼容性问题；
安装npm i -D @babel/core @babel/preset-env babel-loader core-js
进行配置：use里面写入，其中corejs是当ie没有promise这种东西的时候corejs把自己实现的代码引入给他使用，usage表示按需引入；
//配置babel
                {
                    //指定加载器
                    loader: "babel-loader",
                    //设置babel
                    //设置预定义的坏境
                    options: {
                        presets: [
                            [
                                //指定坏境插件
                                "@babel/preset-env",
                                //配置信息
                                {
                                    //targets指定兼容的浏览器版本 corejs指定corejs版本在  
                                    //package.json里面看corejs版本
                                    targets: {
                                        "chrome": "58",
                                        "ie": "11",
                                    },
                                    "corejs": "3",
                                    "useBuiltIns": "usage"
                                }
                            ]
                        ]
                    }
                },
               ...
面向对象简介 类简介
1. 面向对象简介
简单说就是程序中所有操作都需要通过操作对象完成：比如

操作浏览器要使用window对象
操作网页要使用document对象
操作控制台要使用console.log对象
tsc -w 实现自动编译

2. 面向类简介
类--》对象----》模型 总体上这些都是和js一样的，ES6的继承extends super关键字调用父类，抽象类 在前面加关键字：abstract，每个文件使用立即函数，防止变量的冲突，立即函数相当于创建了单独的函数域。

```ts
(function(){
  // 禁止一个类被用来创建对象 抽象类是用来继承的
  //抽象类中可以添加抽象方法
 abstract class Animal{
    name:string;
    constructor(name:string){
      this.name=name;
    }
    //抽象方法 子类必须重写抽象方法
   abstract sayHello():void;
  }
  class Dog extends Animal{
    sayHello(){
      console.log('汪汪');
      
    }
  }
  const dog=new Dog('旺财');
  dog.sayHello();
})();
```
禁止类用来创建对象就是用abstract 抽象类，专门用来继承。抽象方法只能定义在抽象类中，子类必须对抽象方法进行重写。

3. 接口
接口简单理解就是对一些类型的规定，类似于type myType但是又有区别，接口可以重复定义：
```ts
// 接口定义一个类结构
interface myInterface {
  name: string;
  age: number;
}
// interface可以重复定义 
interface myInterface {
  gender: string;
}
//接口的使用
const obj: myInterface = {
  name: 'ddd',
  age: 222,
  gender: 'man',
}
```
接口可以定义类的时候限制类的结构
接口中的所有属性都不能有实际值
接口只定义对象的结构 不考虑实际值 比如用接口去实现一个类，其实就是用接口对类做了一些规范
```ts
interface myInter {
  name: string;
  sayHello():void;
}

// 定义类时 可以使用类去实现一个接口 实现接口就是使类满足接口的要求
//接口就是对类的限制
class MyClass implements myInter {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  sayHello() {
    console.log('Hello~~~');
  }
}
```
4. 属性的封装
属性的封装主要是对属性进行私有化，使得外部不能轻易的改变属性值。

通过关键字来定义私有属性
public 修饰的属性可以在任意位置访问
private 私有属性 私有属性只能在当前类内部进行访问
protected 只能在当前类和继承当前类的类中访问
可以通过在类中添加方法使得私有属性被外部访问 js红宝书有讲怎么访问私有属性可以参考
getter方法用来读取属性
setter方法用来设置属性

```ts
class Person {
   private _name: string;
   private  _age: number;
    constructor(name: string,age: number){
      this._name = name;
      this._age = age;
    }
    // 定义方法用来获取name属性 也可以使用get set 保持属性的使用习惯
    getName() {
      return this._name;
    }
    setName(value: string) {
      this._name = value;
    }
    set age(value: number) {
      this._age = value>0?value: this._age;
    }
  }
  const per = new Person('孙悟空',21);
  console.log(per.getName());
  per.setName('猪八戒');
  per.age=12;
  console.log(per);
  // 下面的写法等价于上面的this的写法
  class C {
    constructor(public name: string, public age: number){

    }
  }
5. 泛型
当类型不明确的时候可以使用泛型比如：

function fn<k>(a:k):k {
  return a;
}
上面里面的k就表示类型，在使用的时候才确定类型，

fn(10);//表示泛型为number
let result2 = fn<string>('hello');//表示指定泛型 为  string
<>里面也可以有两个泛型比如：

function fn2<T,K>(a:T,b:K):T{
  console.log(b);
  return a;
}
fn2<number,string>(123,'hello');
泛型还可以结合接口使用比如：

interface Inter {
  length: number;
}
//表示泛型T必须是Inter实现类
//1
function fn3<T extends Inter> (a:T) {
  return a.length;
}
//2
class MyClass2<T>{
  name: T;
  constructor(name: T){
    this.name = name;
  }
}
```

# JavaScript 代码规范

## 命名规则

### 变量名

- 变量必须使用字母、下划线(\_)或者美元符(\$)开始。
- 然后可以使用任意多个英文字母、数字、下划线(\_)或者美元符(\$)组成
- 不能使用 JS 关键词与保留字。
- 使用小驼峰驼峰命名
- 最好使用 `let const` 命名
- 前缀最好是形容词
- 每次只声明一个变量
```javascript
let firstName = 'John'; // 小驼峰命名 前缀为形容词
const lastName = 'Doe';
let fullPrice = price + price * tax;
let _that = this;
let $ = jQuery;

// bad
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}

// bad 变量在一行声明不便于阅读
let a = 1, b = 2, c = 3;
// good
let a = 1;
let b = 2;
let c = 3;

// 循环和作用域小可以用简写 i, j, k, num, str
```

### 函数

- 使用小驼峰命名

- 前缀最好是动词，可使用动词约定 如： `can has get set load` 等。

  | **动词** | **含义**                     | **返回值**                                            |
  | -------- | ---------------------------- | ----------------------------------------------------- |
  | can      | 判断是否可执行某个动作(权限) | 函数返回一个布尔值。true：可执行；false：不可执行     |
  | has      | 判断是否含有某个值           | 函数返回一个布尔值。true：含有此值；false：不含有此值 |
  | is       | 判断是否为某个值             | 函数返回一个布尔值。true：为某个值；false：不为某个值 |
  | get      | 获取某个值                   | 函数返回一个非布尔值                                  |
  | set      | 设置某个值                   | 无返回值、返回是否设置成功或者返回链式对象            |
  | load     | 加载某些数据                 | 无返回值或者返回是否加载完成的结果                    |

```javascript
// 是否可阅读
canRead() {
  return true;
}

// 获取名称
getName() {
  return this.name;
}
```

### 常量

- 命名方法：名称全部大写。
- 使用大写字母和下划线来组合命名，下划线用以分割单词。

示例：

```javascript
let MAX_COUNT = 10;
let URL = 'http://www.baidu.com';
```

### 构造函数

> 介绍：在 `JS` 中，构造函数也属于函数的一种，只不过采用 `new` 运算符创建对象。

- 命名方法：大驼峰式命名法，首字母大写。
- 命名规范：前缀为名称。

```javascript
function Student(name) {
  this.name = name;
}

let st = new Student('tom');
```

### 类的成员

- 公共属性和方法：跟变量和函数的命名一样。
- 私有属性和方法：前缀为\_(下划线)，后面跟公共属性和方法一样的命名方式。

  ```javascript
  function Student(name) {
    let _name = name; // 私有成员

    // 公共方法
    this.getName = function() {
      return _name;
    };

    // 公共方式
    this.setName = function(value) {
      _name = value;
    };
  }
  let st = new Student('tom');
  st.setName('jerry');
  console.log(st.getName()); // => jerry：输出_name私有变量的值
  ```

## 注释的使用规则。

### 单行注释

> 说明：单行注释以两个斜线开始，以行尾结束。
> 语法：// 这是单行注释

- 单独一行：//(双斜线)与注释文字之间保留一个空格。
- 在代码后面添加注释：//(双斜线)与代码之间保留一个空格，并且//(双斜线)与注释文字之间保留一个空格。
- 注释代码：//(双斜线)与代码之间保留一个空格。

  > 示例：

```javascript
// 调用了一个函数；1)单独在一行
setTitle();

let maxCount = 10; // 设置最大量；2)在代码后面注释

// setName(); // 3)注释代码
```

### 多行注释

> 说明：以/\*开头，\*/结尾
> 语法：/\* 注释说明 \*/

- 若开始(/\*)和结束(\*/)都在一行，推荐采用单行注释。
- 若至少三行注释时，第一行为/\*，最后行为\*/，其他行以\*开始，并且注释文字与\*保留一个空格。

```javascript
/*
 * 代码执行到这里后会调用setTitle()函数
 * setTitle()：设置title的值
 */
setTitle();
```

### 函数方法注释注释

> 说明：函数(方法)注释也是多行注释的一种，但是包含了特殊的注释要求。
> 语法：

```javascript
/**
 * 函数说明
 * @关键字
 */
```

> 常用注释关键字：(只列出一部分，并不是全部)其他常用规范……

| 注释名   | 语法                                      | 含义                 | 示例                                         |
| -------- | ----------------------------------------- | -------------------- | -------------------------------------------- |
| @param   | @param 参数名 {参数类型} 描述信息         | 描述参数的信息       | @param name {String} 传入名称                |
| @return  | @return {返回类型} 描述信息               | 描述返回值的信息     | @return {Boolean} true:可执行;false:不可执行 |
| @author  | @author 作者信息 [附属信息：如邮箱、日期] | 描述此函数作者的信息 | @author 张三 2015/07/21                      |
| @version | @version XX.XX.XX                         | 描述此函数的版本号   | @version 1.0.3                               |
| @example | @example 示例代码                         | 演示函数的使用       | @example setTitle('测试')                    |

> 示例：

```javascript
/**
 * 合并Grid的行
 * @param {Grid} grid 需要合并的Grid
 * @param {Array} cols 需要合并列的Index(序号)数组；从0开始计数，序号也包含。
 * @param {Boolean} isAllSome 是否2个tr的cols必须完成一样才能进行合并。true：完成一样；false(默认)：不完全一样
 * @return void
 * @author polk6 2015/07/21
 * @example
 * _________________                             _________________
 * |  年龄 |  姓名 |                             |  年龄 |  姓名 |
 * -----------------      mergeCells(grid,[0])   -----------------
 * |  18   |  张三 |              =>             |       |  张三 |
 * -----------------                             -  18   ---------
 * |  18   |  王五 |                             |       |  王五 |
 * -----------------                             -----------------
 */
mergeCells(grid, cols, isAllSome) {
  // Do Something
}
```

## 语句的规则

> 简单语句的通用规则:

- 一条语句通常以分号作为结束符。

```javascript
let values = ['Volvo', 'Saab', 'Fiat'];

let person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 50,
  eyeColor: 'blue'
};
```

> 复杂语句的通用规则:

- 将左花括号放在第一行的结尾。
- 左花括号前添加一空格。
- 将右花括号独立放在一行。
- 不要以分号结束一个复杂的声明。

```javascript
// 函数
toCelsius(fahrenheit) {
  return (5 / 9) * (fahrenheit - 32);
}

// 循环
for (let i = 0; i < 5; i++) {
  x += i;
}


// 条件语句不要简写一行
// 正确的写法
if (foo) {
  return bar();
} else {
  something();
}

// 错误的写法 简写阅读性不强
if (foo) return bar();
else something();
```

## 对象规则

> 对象定义的规则:

- 将左花括号与类名放在同一行。
- 冒号与属性值间有个空格。
- 字符串使用单引号，数字不需要。
- 最后一个属性-值对后面不要添加逗号。
- 将右花括号独立放在一行，并以分号作为结束符号

  > 实例:

```javascript
let person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 50,
  eyeColor: 'blue'
};
```

> 短的对象代码可以直接写成一行:

```javascript
let person = { firstName: 'John', lastName: 'Doe', age: 50, eyeColor: 'blue' };
```

> 为了便于阅读每行字符建议小于数 80 个
> 实列：

```javascript
document.getElementById('demo').innerHTML 
  = 'Hello Runoob.';
```

## 其他规则

### 空格规则

- 规范随后指出应该使用 2 个，而不是 4 个空格带实现缩进。

```javascript
// bad
function foo() {
∙∙∙∙let name;
}

// bad
function bar() {
∙let name;
}

// good
function baz() {
∙∙let name;
}
```

- 每个语句必须以分号结尾。

```javascript
// bad
let luke = {}
let leia = {}
[(luke, leia)].forEach(jedi => (jedi.father = 'vader'))
// good
let luke = {};
let leia = {};
[luke, leia].forEach(jedi => {
  jedi.father = 'vader';
});
```
- 代码不要有多余的空格
```javascript
// bad
{
  tiny:   42,  
  longer: 435, 
};
// good
{
  tiny: 42, 
  longer: 435,
};
```
- 优先使用箭头函数

  > 箭头函数提供了一种简洁的语法，并且避免了一些关于this指向的问题。相比较与function关键字，开发者应该优先使用箭头函数来声明函数，尤其是声明嵌套函数。
```javascript
// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```
- 优先使用for...of

```javascript
for (let k of obj) {

}
```

- 不要使用eval语句

```javascript
// bad
let obj = { a: 20, b: 30 };
let propName = getPropName();  // returns "a" or "b"
eval( 'var result = obj.' + propName );
// good
let obj = { a: 20, b: 30 };
let propName = getPropName();  // returns "a" or "b"
let result = obj[ propName ];  //  obj[ "a" ] is the same as obj.a
```




# TypeScript代码规范

> Typescript是javascript的超集，所以ts在运行之前，得先编译成js，那么这个编译的过程，ts的编译引擎就得知道，文件里包括哪些方法，方法包含哪些参数，各参数的定义是什么，类型是什么，总之，所有源信息必须都知道，才能准确无误的把ts翻译成js。这些东西也正是我们需要的，通过这些信息，我们就可以对比规范和源信息，来确认是否是符合我们制定规范的代码。

## 命名

- 使用PascalCase为类型命名。
- 不要使用I做为接口名前缀。
- 使用PascalCase为枚举值命名。
- 使用camelCase为函数命名。
- 使用camelCase为属性或本地变量命名。
- 不要为私有属性名添加_前缀。
- 命名时尽可能地使用全名（而非缩写）
```typescript
// 定义枚举
const enum StateEnum {
  TO_BE_DONE = 0,
  DOING = 1,
  DONE = 2
}

// 定义 item 接口
interface SrvItem {
  val: string,
  key: string
}

// 定义服务接口
interface SrvType {
  name: string,
  key: string,
  state?: StateEnum,
  item: Array<SrvItem>
}

// 然后定义初始值（如果不按照类型来，报错肯定是避免不了的）
const types: SrvType = {
  name: '',
  key: '',
  item: []
}

```

## 风格

- 使用箭头函数（arrow function，即 lambda 表达式）代替匿名函数
```typescript
 x => x + x;
 (x,y) => x + y;
 (x: T, y: T) => x === y;
```
- 仅当必要时才在箭头函数的参数列表中使用括号。例如：
- 总是使用大括号括起循环体和条件体

```typescript
// 正确的写法
if (foo) {
  return bar();
} else {
  something();
}

// 错误的写法 简写阅读性不强
if (foo) return bar(); else something();
```
- 使用2个空格进行缩紧

## 类型

- 除非类型/函数需要在多个组件中共享，否则不要导出(export)
- 在文件中，类型定义应该放在最前面
- 不要使用如下类型Number，String，Boolean或Object。 这些类型指的是非原始的装盒对象，它们几乎没在JavaScript代码里正确地使用过。
```typescript
// bad

function reverse(s: String): String {
  
};

function reverse(s: string): string {

};

```
- 为返回值忽略的回调函数设置void类型的返回值

```typescript
function hello(): void {
  alert("Hello Runoob");
}
```
- 可以使用 泛型 来创建可重用的组件。比如你想创建一个参数类型和返回值类型是一样的通用方法

```typescript
function foo<T> (arg: T): T {
  return arg
}
let output = foo('string') // type of output will be 'string'
```

## 注释

- 为函数、接口、枚举和类使用 JSDoc 风格的文档注释，和javascript注释差不多。

## 字符串

- 使用单引号括起字符串

```typescript

const hello: string = 'Hello World!'

```

> 代码编写完成后，使用tslint检查代码



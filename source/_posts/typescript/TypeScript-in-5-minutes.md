---
title: TypeScript in 5 minutes
p: typescript/TypeScript-in-5-minutes
date: 2018-07-28 22:26:40
tags: TypeScript
categories: 前端
---

首要步骤安装TypeScript:

可以参考本系列中 {%  post_link typescript/TypeScript安装与配置   %}

## Building your first TypeScript file

安装完成后在编辑器中创建一个 greeter.ts:

```typescript
function greeter(person){
    return "Hello, " + person;
}
let user = "Jane User";
console.log(greeter(user))
```

在命令行中输入

```bash
tsc greeter.ts
```

此命令将 greeter.ts 文件编译成greeter.js文件，以目前的代码来说编译出来的js文件与ts文件相同。

## Type annotations

为greeter.ts增加 typescript类型,为greeter方法的参数person增加 :string 类型注解

```typescript
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";
console.log(greeter(user))
```

类型注解是typescript中用于表示函数或变量的期望类型，在本例中 greeter接收一个名为person的string变量，将本例中代码修改：

```typescript
function greeter(person: string) {
    return "Hello, " + person;
}

let user = [0,1,2];
console.log(greeter(user))
```

重新编译你将得到一个编译时错误:

```typescript
TSError: ⨯ Unable to compile TypeScript:
tsdemo-chapter/greeter.ts(7,21): error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'.
```

扩展一下，如果将代码中的user修改为 如下的非string 会出现什么情况:

```typescript
function greeter(person: string) {
    return "Hello, " + person;
}

let user;
let user2 = undefined;
let user3 = null;
console.log(greeter(user))
console.log(greeter(user2))
console.log(greeter(user3))
```

重新编译，上述代码将编译通过，并可以执行输出如下内容

```typescript
Hello,undefined
Hello,undefined
Hello,null
```

依据上述实验可以看出typescript在默认的情况 `undefined` 与`null`可以做为任何的类型的变量值。

除了参数类型外，参数的个数也会在编译的时候进行检查。

```typescript
consloe.log(greeter("abc","def"))
```

重新编译后将会抛出如下错误

```typescript
error TS2554: Expected 1 arguments, but got 2.
```

typescript可以通过静态代码分析代码在编译期间即找出错误，如上面例子中的类型不匹配，参数个数不相符等问题，这些问题可以在编译期间发现。`需要注意的是即使编译期间发现错误，ts仍然会编译为js文件。`

## Interface

接下来我们顶一个具有firstName与lastName的 interface。在Typescript如果有两种类型的内部结构是相兼容的则这两种类型是兼容的。这样就不需要在定义接口后再 使用implements去实现接口。

```typescript
interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Jane", lastName: "User" };

console.log(greeter(user));
```

## Classes

 TypeScript支持JavaScript的新特性，比如支持基于类的面向对象编程。接下来创建一个`Student`类带有一个constructor和一些公共的字段。类和接口可以一起协作，程序员可以自己定义抽象级别。

`在构造函数的参数上使用pulibc 等同于创建了同名的成员变量`

```typescript
class Student {
    fullName: string;
    constructor(public firstName: string, public middleInitial: string, public lastName: string) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person : Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}
let user = new Student("Jane", "M.", "User");

console.log(greeter(user))
```

重新编译greeter.js，你会看到与之前相似的javascript代码，Typescript使用 javascript中的 prototype-base OO 

来实现Classes。编译后的javascript代码 interface 等javascript并不支持的语法已经被檫除。

```javascript
function greeter(person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}
var Student = /** @class */ (function () {
    function Student(firstName, middleInitial, lastName) {
        this.firstName = firstName;
        this.middleInitial = middleInitial;
        this.lastName = lastName;
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
    return Student;
}());
var user = new Student("Jane", "M.", "User");
console.log(greeter(user));
```


# 类

传统的 JS 程序使用函数和基于原型（prototype）继承来创建可重用的“类”，这对于面向对象编程来说很不友好。在 ES6 新增了对 `class` 语法糖的支持，而 TS 在 ES6 的语法上又进行了扩展，使面向对象编程更加的简单容易。

## 创建类

在 TS 中和 ES6 一样，都是使用 `class` 来创建类：

```ts
class Animal {
  name: string;
  age: number;
  constructor(
    name: string
  ) {
    this.name = name;
  }
  getName(): void {
    console.log(this.name);
  }
  getAge(): void {
    console.log(this.age);
  }
  setAge(age: number): void {
    this.age = age;
  }
}
```

上面声明一个类 `Animal` ，这个类有六个类成员：类属性 `name`/`age` 、构造函数 `constructor` 以及方法 `getName`/`getAge`/`setAge`,其中类属性可以通过 this.name/age 来访问,下面实例化一个 Animal 的新对象，并执行构造函数初始化。

```ts
let tidy = new Animal("tidy");
tidy.setAge(2);
tidy.getAge();  // 2
```

## 继承和多态

封装、继承和多态是面向对象的三大特性。上面的例子中把设置动物的年龄写到一个类中，即所谓的封装。在 TS 中，使用 extends 关键字即可方便的实现继承：

```ts
class Bird extends Animal {
  color: string;
  constructor(name: string) {
    super(name);
  }
  setAge(age: number) {
    this.age = age;
    console.log(this.age);
  }
  setColor(color: string): void {
    this.color = color;
  }
  getColor(): void {
    console.log(this.color);
  }
}
let Suzaku = new Bird('Suzaku');
Suzaku.setAge(3);  // 3
console.log(Suzaku.name);  // Suzaku
Suzaku.setColor('red');
Suzaku.getColor();  // red
```

以上，Bird 是基类 Animal 的子类，通过 extends 来继承父类的属性和方法，也可以重写父类的属性和方法，这样父类的方法在不同的类中就有不同的功能，这就是多态。

派生类构造函数必须调用 `super()` 来执行基类的构造方法。

## 修饰符

在类中的修饰符可以分为公共( punlic )、私有( private ) 和受保护 ( protected ) 三种类型：

### public

在 TS 中，每个成员默认为 public ， 可以被自由的访问。也可以显式的给定义的成员加上 public 修饰符。

### private

当类的成员被标记为 private 时，就不能在累的外部访问它。

```ts
Suzaku.name;  // error TS2341: Property 'name' is private and only acce
```

>ES6 中并没有提供对私有属性的语法支持，但是可以通过闭包来实现私有属性。

### protected

protected 修饰符与 private 修饰符的行为很相似，但有一点不同，private 成员在派生类中仍然可以访问。

## 参数属性


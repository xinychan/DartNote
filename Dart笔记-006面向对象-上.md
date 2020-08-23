# 面向对象

Dart 是一种基于类和 mixin 继承机制的面向对象的语言；

每个对象都是一个类的实例，所有的类都继承于 Object；

## 类与对象

使用关键字 class 声明类

使用关键字 new 创建一个对象，new 可以省略

所有对象都继承于 Object 类

    /**
    * 属性默认会生成 getter/setter 函数
    * 使用 final 声明的属性只有 getter 函数
    * 函数不能被重载
    */
    class Person {
        String name;
        String feature;
        final String code = "code";

    void work() {
        print("work");
    }

    // 函数不能被重载；函数名唯一，不能重复使用
    void work2(String name) {
        print("work2");
    }
    }

    // 类的创建和使用
    var person = Person();
    person.name = "Dart";
    person.feature = "Hello";
    person.work();

## 类及成员的可见性

Dart 中可见性以 library（库） 为单位

默认情况下，每一个 Dart 文件就是一个库

使用下划线 \_ 表示库的私有

使用 import 导入库

    class Phone {
        String name;
        // 私有属性
        String _feature;
    }

    // 类的使用
    import 'phone.dart';
    void main() {
        var phone = Phone();
        phone.name = "Android";
    }

## 计算属性

    /**
    * 计算属性
    */
    class Rect {
        num width;
        num height;

        // 计算属性；使用 get 标识计算属性
        num get area {
            return width * height;
        }

        // 计算属性；使用 set 处理计算属性
        set area(value) {
            width = value / height;
        }
    }

    /**
    * 计算属性的使用
    */
    var rect = Rect();
    // 计算属性的获取
    rect.width = 10;
    rect.height = 20;
    print(rect.area);
    // 通过计算属性来获取其他属性
    rect.area = 600;
    print(rect.width);

## 构造函数

    /**
    * 构造函数
    */
    class People {
        String name;
        int age;

        final String action;

        // final 变量需要初始化；如果没有初始化，可以在构造函数中初始化
        People(this.name, this.age, this.action) {
            // 通过 this 关键字，直接将传入参数赋值给全局变量
            print("People action = $action");
        }

        // 构造函数不能被重载；如果构造函数名称已经使用，需要使用命名构造函数
        People.withName(String name, this.action) {
            this.name = name;
            print("People withName = $name");
        }

        void work() {
            print("People work");
        }
    }

## 常量构造函数

    /**
    * 常量构造函数
    * 如果类是不可变状态，可以把对象定义成编译期常量
    */
    class User {
        final String name;
        final int age;

        // 使用 const 声明构造函数，并且所有变量为 final
        // 常量构造函数不允许有函数体
        const User(this.name, this.age);
    }

    // 常量构造函数的使用：使用对象作为常量，对象需要使用常量构造函数
    const user = const User("name", 20);

## 工厂构造函数

    /**
    * 工厂构造函数
    * 普通构造函数没有return语句，工厂构造函数可以return对象
    * 使用 factory 修饰构造函数
    */
    class Player {
        String name;

        factory Player(String name) {
            return Player._withName(name);
        }

        Player._withName(this.name);
    }

    // 使用工厂构造函数
    var player = Player("name");

## 初始化列表

    /**
    * 初始化列表
    * 初始化列表会在构造函数体执行之前执行
    * 初始化列表常用于给 final 变量赋值
    */
    class People {
        String name;
        int age;

        final String action;

        People(this.name, this.age, this.action);

        // 初始化列表给变量赋值
        People.withMap(Map map) : name = map["name"], action = map["action"] {
            this.age = map["age"];
        }
    }

## 静态成员

    /**
    * 静态成员
    * 静态成员不能访问非静态成员，非静态成员可以访问静态成员
    * 类中的常量需要使用 static const 声明
    */
    class People {
        static const String TAG = "People";
        static String name;
        int age;

        // 不能访问 age
        static void workName() {
            print("work name:$name");
        }

        // 能访问 age 和 name
        void workAge() {
            print("work name:$name");
            print("work name:$age");
        }
    }

## 对象操作符

非空运算符

    // 非空运算符 ?.
    String name;
    // 只有当 name 变量不为 null 才会执行后续逻辑
    name?.length;

类型转换

    // 类型转换 as
    var action;
    action = 10;
    action = "action";
    (action as String).length;

类型判断

    // 类型判断 is / is!
    var action2;
    action2 = 20;
    action2 = "action2";
    if (action2 is String) {
        print(action2.length);
    }
    if (action2 is! int) {
        print(action2);
    }

级联操作

    // 级联操作
    var people = People();
    people..name = "name"
          ..age = 20
          ..work();

## 对象 Call 函数

    /**
    * 对象Call函数
    * 如果类实现了Call函数，则该类对象可以作为函数使用
    */
    class People {
        String name;
        int age;

        void call() {
            print("People Call");
        }
    }

    // 类当成函数使用
    var people = People();
    people();
    people.call();

## 继承

使用 extends 关键字继承类

子类会继承父类可见属性和函数，不会继承构造函数

子类能复写父类函数

单继承，多态性

    class Animal {
        String name;

        void eat() {
            print("Animal eat");
        }
    }

    class Cat extends Animal {
        void miao() {
            print("Cat miao");
        }
    }

    // 子类的使用
    var cat = Cat();
    cat.name = "jiafei";
    cat.eat();

## 继承中的构造函数

子类构造函数默认调用父类无名无参构造函数

如果父类没有无名无参构造函数，子类需要显式调用父类构造函数

    class Animal {
        String name;
        // 父类构造函数在子类构造函数体开始执行时调用
        Animal(this.name);
        Animal.withName(this.name);
    }

    class Cat extends Animal {
        final String type;

        // 父类没有无名无参构造函数，子类构造函数，需要显式调用父类构造函数
        // 如果有初始化列表，初始化列表会在父类构造函数之前执行
        Cat(String name, String type) : this.type = type, super.withName(name);
    }

## 抽象类

抽象类使用 abstract 关键字表示，不能直接被实例化

抽象函数不用 abstract 修改，无具体实现

抽象类可以没有抽象函数

有抽象函数的类必须是抽象类

    abstract class Animal {
        void eat();
    }

    class Cat extends Animal {
        @override
        void eat() {
            print("Cat eat");
        }
    }

## 接口

类和接口是统一的，类就是接口

每个类都隐式定义了一个包含所有实例成员的接口

复用已有类的实现，使用继承方式；使用已有类的外在行为，使用接口方式

    class Animal {
        String name;

        void eat() {
            print("Animal eat");
        }
    }

    class Cat implements Animal {
        // 实现类的接口，需要重写所有成员变量和函数
        @override
        String name;

        @override
        void eat() {
            print("Cat eat");
        }
    }

# 面向对象

## Mixin

Mixin 类似多继承，是在多类继承中重用类代码的方式;

通过创建一个继承自 Object 且没有构造函数的类，来实现 一个 Mixin;

如果 Mixin 不希望作为常规类被使用，使用关键字 mixin 替换 class;

    class Action1 {
        void func1() {
            print("Action1 func1");
        }
    }

    mixin Action2 {
        void func2() {
            print("Action2 func2");
        }
    }

    mixin Action3 {
        void func3() {
            print("Action3 func3");
        }
    }

    /**
    * Mixin
    * 使用 with 关键字连接 Mixin
    * 子类使用 Mixin 后，可以使用多个 Mixin 类中的函数
    * 如果多个 Mixin 中有函数名相同的函数，子类使用最后的一个 Mixin 中同名函数
    * 作为 Mixin 的类不能有显式的构造函数
    * 作为 Mixin 的类只能继承自 Object
    */
    class ActionDemo with Action1, Action2, Action3 {}

    // 子类使用 Mixin 中的函数
    var action = ActionDemo();
    action.func1();
    action.func2();
    action.func3();

指定只有某些类型可以使用的 Mixin,使用 on 来指定可以使用 Mixin 的父类类型;

    mixin MusicalPerformer on Musician {
        // 只有 Musician 的子类才能使用该 Mixin
    }

## 运算符重载

运算符重载需要在类中定义；使用 operator 关键字重载运算符

    class People {
        int age;

        People(this.age);

        // 使用 operator 重写操作符
        bool operator >(People people) {
            return this.age > people.age;
        }

        int operator [](String str) {
            if (str == "age") {
                return this.age;
            }
            return 0;
        }
    }

    // 使用重载的运算符
    var p1 = People(15);
    var p2 = People(18);
    print(p2 > p1);
    print(p2["age"]);

## 枚举

使用 enum 关键字定义枚举

枚举的 index 从 0 开始，依次累加

枚举不可以指定 index 值

枚举中不允许有函数

    enum Action {
        eat,
        drink,
        play,
        happy }

    // 使用枚举
    var action = Action.play;
    switch (action) {
        case Action.eat:
        print("eat");
        break;
        case Action.drink:
        print("drink");
        break;
        case Action.play:
        print("play");
        break;
        case Action.happy:
        print("happy");
        break;
    }

## 泛型

使用泛型限制使用指定类型

    // 类的泛型
    class Demo<T> {
        T entry;

        void putEntry(T entry) {
            this.entry = entry;
        }

        // 函数的泛型
        void putItem<E>(E item) {
            print(item);
        }
    }

    // 泛型的使用
    var demo = Demo<int>();
    demo.putEntry(10);
    demo.putItem("item");

泛型用于集合中的参数化字面量

    // 使用泛型声明集合元素类型
    var names = <String>['Seth', 'Kathy', 'Lars'];
    var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
    var pages = <String, String>{
        'index.html': 'Homepage',
        'robots.txt': 'Hints for web robots',
        'humans.txt': 'We are people, not machines'
    };

Dart 中泛型类型是固化的，也就是说它们在运行时是携带着类型信息的；在运行时可以检测集合的类型；

    var names = List<String>();
    names.addAll(['Seth', 'Kathy', 'Lars']);
    print(names is List<String>); // true

> 相反，Java 中的泛型会被擦除 ，也就是说在运行时泛型类型参数的信息是不存在的。在 Java 中，可以测试对象是否为 List 类型，但无法测试它是否为 `List<String>`

## 异步支持

使用 async 和 await 关键字实现异步编程；可以像编写同步代码一样实现异步操作；

async 让函数成为异步函数，await 等待异步函数执行完成；

只有 async 函数才能使用 await 关键字来调用函数；

调用 async 函数，必须使用 await 关键字；

    // 异步函数泛型类型为 Future；可使用泛型限制返回值类型
    Future<String> funcAsync() async {
        return "funcAsync";
    }

    // 如果异步函数没有返回有效值，需要设置其返回类型为 Future<void>
    Future<void> funcAsync2() async {
        print("funcAsync2");
    }

    // 省略返回值，则返回值类型为 dynamic
    funcAsync3() async {
        print("funcAsync3");
    }

    // await 函数必须在 async 函数中调用
    void main() async {
        // 使用 await 关键字调用异步函数，此时 result 类型为 String
        var result = await funcAsync();
        print(result);
        // result2 类型为 void
        var result2 = await funcAsync2();
        // print(result2);
        // result3 类型为 dynamic
        var result3 = await funcAsync3();
        print(result3);
    }

## 异常

Dart 代码可以抛出和捕获异常。异常表示一些未知的错误情况。

如果异常没有被捕获，则异常会抛出，导致抛出异常的代码终止执行。

和 Java 有所不同，Dart 中的所有异常是非检查异常。方法不会声明它们抛出的异常，也不要求捕获任何异常。

Dart 提供了 Exception 和 Error 类型，以及一些子类型。当然也可以定义自己的异常类型。

但是，此外 Dart 程序可以抛出任何非 null 对象，不仅限 Exception 和 Error 对象。

throw:

    // 下面是关于抛出或者引发异常的示例
    throw FormatException('Expected at least 1 section');

    // 也可以抛出任意的对象
    throw 'Out of llamas!';

catch:

捕获异常可以避免异常继续传递（除非重新抛出（rethrow）异常）

通过指定多个 catch 语句，可以处理可能抛出多种类型异常的代码。

与抛出异常类型匹配的第一个 catch 语句处理异常。

如果 catch 语句未指定类型，则该语句可以处理任何类型的抛出对象。

    try {
        breedMoreLlamas();
    } on OutOfLlamasException {
        // 一个特殊的异常
        buyMoreLlamas();
    } on Exception catch (e) {
        // 其他任何异常
        print('Unknown exception: $e');
    } catch (e) {
        // 没有指定的类型，处理所有异常
        print('Something really unknown: $e');
    }

如上述代码所示，捕获语句中可以同时使用 on 和 catch，也可以单独分开使用。

使用 on 来指定异常类型，使用 catch 来 捕获异常对象。

catch() 函数可以指定 1 到 2 个参数，第一个参数为抛出的异常对象，第二个为堆栈信息(一个 StackTrace 对象)。

    try {
        // ···
    } on Exception catch (e) {
        print('Exception details:\n $e');
    } catch (e, s) {
        print('Exception details:\n $e');
        print('Stack trace:\n $s');
    }

如果仅需要部分处理异常， 那么可以使用关键字 rethrow 将异常重新抛出。

    void misbehave() {
        try {
            dynamic foo = true;
            print(foo++); // Runtime error
        } catch (e) {
            print('misbehave() partially handled ${e.runtimeType}.');
            rethrow; // Allow callers to see the exception.
        }
    }

    void main() {
        try {
            misbehave();
        } catch (e) {
            print('main() finished handling ${e.runtimeType}.');
        }
    }

finally:

不管是否抛出异常，finally 中的代码都会被执行。如果 catch 没有匹配到异常，异常会在 finally 执行完成后，再次被抛出。

    try {
        breedMoreLlamas();
    } finally {
        // Always clean up, even if an exception is thrown.
        cleanLlamaStalls();
    }

任何匹配的 catch 执行完成后，再执行 finally。

    try {
        breedMoreLlamas();
    } catch (e) {
        print('Error: \$e'); // Handle the exception first.
    } finally {
        cleanLlamaStalls(); // Then clean up.
    }

## Isolates

大多数计算机中，甚至在移动平台上，都在使用多核 CPU。为了有效利用多核性能，开发者一般使用共享内存数据来保证多线程的正确执行。然而，多线程共享数据通常会导致很多潜在的问题，并导致代码运行出错。

所有 Dart 代码都在隔离区（isolates）内运行，而不是线程。每个隔离区都有自己的内存堆，确保每个隔离区的状态都不会被其他隔离区访问。

## Typedefs

使用 typedef，或者 function-type alias 为函数起一个别名，别名可以用来声明字段及返回值类型。

当函数类型分配给变量时，typedef 会保留类型信息。

    // 声明函数类型为 int Function(int)
    typedef funcType = int Function(int);

    void main() {
        // act1 类型为 int Function(int)
        var act1 = (int index) {
            return index;
        };
        // 使用对象的 runtimeType 属性，可以在运行时获取对象的类型
        print(act1.runtimeType); // (int) => int
        // 只能判断 act1 是否为 Function，参数和返回值类型信息丢失
        print(act1 is Function); // true
        // 使用 typedef 可以具体判断 act1 的参数和返回值类型
        print(act1 is funcType); // true
    }

## 注解

注解以字符 @ 开头，后跟对编译时常量(如 deprecated)的引用或对常量构造函数的调用；

对于所有 Dart 代码有两种可用注解：@deprecated 和 @override；

使用反射可以在运行时获取注解信息；

    // 自定义注解
    class Todo {
        final String who;
        final String what;

        // 要被当成注解使用，构造方法必须是 const
        const Todo(this.who, this.what);
    }

    @Todo("who", "what")
    void doSomething() {
        print("doSomething");
    }


> 参考资料
> 慕课网：Flutter开发第一步-Dart编程语言入门
> [Dart 编程语言中文网](https://www.dartcn.com/guides/language/language-tour)
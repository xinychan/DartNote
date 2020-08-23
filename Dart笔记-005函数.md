# 函数

Dart 中的函数也是对象，并且有具体类型为 Function；

返回值类型，参数类型都可以省略；

箭头语法： => expr 是 return expr 简写；适用于一个表达式的场景

所有函数都会返回一个值；如果没有明确指定返回值，函数体会被隐式的添加 return null; 语句

## 函数的定义

    /**
     * String:函数返回值类型
     * funcDemo:函数名
     * String name:函数参数
     * return:函数返回值
     */
    String funcDemo(String name) {
      print("funcDemo:$name");
      return "funcDemo";
    }

    void funcDemo1(String name) {
      print("funcDemo1:$name");
      // 无返回值，默认也有一句 return null 结尾；return null 可省略
      return null;
    }

    String funcDemo2(String name) {
      print("funcDemo2:$name");
      // 如果没有声明返回值，默认都有一句 return null 结尾；return null 可省略
      // return null;
    }

    /**
     * 省略返回值；则返回值类型为 dynamic
     * 省略参数类型；则参数类型为 dynamic
     */
    funcDemo3(name) {
      print("funcDemo3:$name");
      return "funcDemo3";
    }

    /**
     * 使用 => 表达式
     * 无返回值
     */
    funcDemo4(String name) => print("funcDemo4:$name");

    /**
     * 使用 => 表达式
     * 有返回值
     */
    String funcDemo5(String name) => "funcDemo5:$name";

## 可选参数

可选命名参数：

    /**
    * 可选命名参数
    * {}内为可选命名参数，可不传，默认为 null
    */
    void funcDemo6(String name, {int code, int number}) {
      print("name = $name,code = $code,number = $number");
    }

    // 调用时使用参数名称
    funcDemo6("funcDemo6");
    funcDemo6("funcDemo6", code: 60, number: 10);

可选位置参数：

    /**
    * 可选位置参数
    * []内为可选位置参数，可不传，默认为 null
    */
    void funcDemo7(String name, [int code, int number]) {
      print("name = $name,code = $code,number = $number");
    }

    // 调用时使用参数位置
    funcDemo7("funcDemo7");
    funcDemo7("funcDemo7", 80, 100);

## 默认参数

    /**
    * 默认参数；在可选参数中，可以给参数赋默认值
    * 使用 = 给参数赋默认值
    * 默认参数值只能是编译期常量
    */
    void funcDemo8(String name, {int code = 100, int number = 100}) {
      print("name = $name,code = $code,number = $number");
    }

    // 使用时与可选参数一致
    funcDemo8("funcDemo8");
    funcDemo8("funcDemo8", code: 50, number: 60);

## 函数对象

函数可作为对象赋值给其他变量

函数可作为参数传递给其他函数

    void funcPrint() {
      print("funcPrint");
    }

    // 赋值与调用
    Function funcDemo = funcPrint;
    funcDemo.call();
    funcDemo();

## 匿名函数

    // 匿名函数；只有参数和具体实现
    var funcDemo = () {
      print("funcDemo");
    };
    funcDemo.call();

## 闭包

闭包是一个函数；

闭包定义在其他函数内部；

闭包能访问外部函数内的局部变量，并持有状态；

    Function funcClosure() {
      int index = 0;

      // 闭包可以使用外部函数中的参数
      printIndex() {
        index++;
        print("printIndex:$index");
      }

      return printIndex;
    }

    // 闭包的使用
    var func = funcClosure();
    func.call();
    func.call();
    func.call();

## 自执行函数

    // 不需要主动调用就会执行的函数
    (() {
      print("自执行函数");
    })();

    // 传入参数的自执行函数
    ((int index) {
      print(index);
      print("自执行函数");
    })(100);

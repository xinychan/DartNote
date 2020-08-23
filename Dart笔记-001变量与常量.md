# 变量与常量

在 Dart 中，任何保存在变量中的都是一个对象，并且所有的对象都是对应一个类的实例；

无论是数字，函数和 null 都是对象。所有对象继承自 Object 类；

尽管 Dart 是强类型的，但是 Dart 可以推断类型，所以类型注释是可选的；

如果要明确说明不需要任何类型， 需要使用特殊类型 dynamic；

## 变量

使用 dynamic 声明动态类型变量，类型可以为任意类型；

使用 var 声明值可变变量，类型为初始化类型，初始化后类型不可变，值可变；

使用 final 声明值不可变变量，只能被赋值一次；

使用 int/String 等指定类型变量，类型不可变，值可变；

变量未初始化时，默认值为 null；

    // 动态类型变量；可以赋值为任意类型
    dynamic dynVal;
    dynVal = 10;
    dynVal = "dynVal";
    print(dynVal);

    // 值可变变量；未初始化时，值为 null，类型为 dynamic
    var action;
    action = 100;
    action = "Dart";
    print(action);

    // 值可变变量；已初始化时，则类型为初始化类型，类型不可变
    var action1 = 100;
    action1 = 101;
    // action1 = "Dart"; 类型不再可变，只能赋同类型值
    print(action1);

    // 值不可变变量；只能赋值一次
    final action2 = 100;
    print(action2);

    // 指定类型变量；只能赋值指定类型
    int action3;
    // 未初始化，值为 null
    print(action3);
    action3 = 101;
    print(action3);

    // 常量的值只能赋值一次，且必须是编译期常量
    const action4 = 200;

## 常量

使用 const 声明常量；

使用 const 声明的必须是编译期常量；

Const 变量是隐式 Final 的类型；

提示：实例变量可以是 final 类型但不能是 const 类型；必须在构造函数体执行之前初始化 final 实例变量：在变量声明中，参数构造函数中或构造函数的初始化列表中进行初始化

    // const 常量
    const action4 = 200;

    // final 可以开始不赋值，但只能赋值一次；final 是运行时常量，在运行时第一次使用才初始化
    final time = new DateTime.now();

    // const 初始化时必须赋值，且必须是编译期常量；const 常量无法这样赋值
    // const time = new DateTime.now();

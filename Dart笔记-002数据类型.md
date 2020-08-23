# 数据类型

## 常用内置类型

数值型-Number

字符串-String

布尔型-Boolean

列表-List

键值对-Map

Set 集合（Dart2.2）

## 数值型

num 类型包含整型与浮点型

    // num 类型包含 int/double 类型
    num numVal = 10; // int 类型
    numVal = 1.5; // double 类型
    // int 类型
    int intVal = 10;
    intVal = 11;
    // double 类型
    double douVal = 10.5;
    douVal = 10.5;

    // num 类型的转换
    int intVal2 = douVal.toInt();
    double douVal2 = intVal.toDouble();

## 字符串

使用单引号，双引号创建字符串

使用三单引号/三双引号创建多行字符串

使用 r 创建原始 raw 字符串

    // 普通字符串
    String str1 = 'Dart';
    String str2 = "Dart";

    // 多行字符串
    String str3 = """Hello
                         Dart""";
    String str4 = '''Hello
                        Dart''';

    // 普通字符串；\n 表示下一行
    String str5 = 'Hello \n Dart';
    // 原始 raw 字符串；\n 不被转义
    String str6 = r'Hello \n Dart';

    // 插值表达式：${表达式}
    String str7 = "Hello $str1";
    print(str7); // Hello Dart

    // 运算符：+  * == []
    String str8 = "-Hello-";
    String str9 = "-Hello-";
    print(str9 + "Dart"); // 拼接字符串
    print(str9 * 3); // 字符串重复
    print(str9 == str8); // 字符串内容判断
    print(str9[1]); // 字符串下标位置字符

## 布尔型

使用 bool 表示布尔类型

值为 true 或 false

    bool isTrue = true;
    bool isFalse = false;

## 列表

在 Dart 中，数组与列表是同一个概念；

    // 可变 List 创建；默认可添加多个类型
    var list = [0, 1, 2, "dart"];
    list.add(4);
    print(list);
    // 获取 List 中元素
    var listVal = list[3];
    print(listVal);
    // 修改 List 中元素
    list[3] = "Hello";
    print(list[3]);

    // 不可变 List 创建
    var list2 = const [0, 1, 2, "dart"];
    // 不可变 List 不可修改，否则抛出异常：Cannot modify an unmodifiable list
    // list2.add(4);
    // list2[3] = "Hello";
    print(list2);

    // 使用 new 关键字创建
    var list3 = new List<int>();
    list3.add(0);
    list3.add(1);
    list3.add(2);
    // list3.add("dart"); List 指定类型后，不可添加其他类型
    print(list3);

    // 不指定 List 元素类型，可添加其他类型
    var list4 = new List();
    list4.add(0);
    list4.add(1);
    list4.add(2);
    list4.add("dart");
    print(list4);

    // List 循环
    list4.forEach((value) {
        print(value);
    });

    // 修改 List 数据，并返回一个新 List
    var list4map = list4.map((value){
        return value.toString() + "--dart";
    });
    print(list4map); // (0--dart, 1--dart, 2--dart, dart--dart)

    // 筛选符合条件的，并返回一个新 List
    var list4where = list4.where((value){
        return value is int;
    });
    print(list4where); // (0, 1, 2)

    // 集合中有一个符合条件的，则返回 true
    var list4any = list4.any((value){
        return value is String;
    });
    print(list4any); // true

    // 集合中所有元素都符合条件，则返回 true
    var list4every = list4.every((value){
        return value is int;
    });
    print(list4every); // false

## 键值对

Map 中的 Key 和 Value，都可以是不同类型；

    // 创建可变 Map
    var mapVal = {"key0": 0, "key1": "dart", 2: false};
    // 修改元素
    mapVal["key0"] = "map";
    // 添加元素
    mapVal["key3"] = "val3";
    // 获取元素
    print(mapVal[2]); // 打印 false
    print(mapVal);

    // 创建不可变 Map；不允许添加和修改元素
    var mapVal2 = const {"key0": 0, "key1": "dart", 2: true};
    print(mapVal2);

    // 使用 new 关键字创建；指定类型后，Key/Value 类型不可变
    var mapVal3 = new Map<String, String>();
    mapVal3["key0"] = "val0";
    // mapVal3["key1"] = false;
    print(mapVal3);

    // Map 循环
    var func = (key, value) {
      print("key = $key,value = $value");
    };
    mapVal.forEach(func);

## Set 集合

    // 在 Dart 中 Set 是一个元素唯一且无序的集合，不能通过索引获取数据
    // 虽然 Set 类型一直是 Dart 的核心部分， 但在 Dart2.2 中才引入了 Set 字面量
    // 通过字面量创建 Set 的一个简单示例
    var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
    print(halogens); // {1, 2, 3}

    // 要创建一个空集，使用前面带有类型参数的 {} ，或者将 {} 赋值给 Set 类型的变量
    var names = <String>{};
    // Set<String> names = {}; // 这样也是可以的
    // var names = {}; // 这样会创建一个 Map ，而不是 Set

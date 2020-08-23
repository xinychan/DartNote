# 运算符

## 算数运算符

    int a = 10;
    int b = 2;

    // 加减乘除
    print(a + b);
    print(a - b);
    print(a * b);
    print(a / b);
    // 取整
    print(a ~/ b);
    // 取余
    print(a % b);

## 比较运算符

    // == 用于比较内容
    String str1 = "dart";
    String str2 = "dart";
    print(str1 == str2);

    // 比较运算
    int a = 10;
    int b = 8;
    print(a == b);
    print(a != b);
    print(a > b);
    print(a < b);
    print(a >= b);
    print(a <= b);

## 逻辑运算符

    // 逻辑运算符 ! && ||
    bool trueVal = true;
    bool falseVal = false;
    print(trueVal);
    print(!trueVal);
    print(trueVal && falseVal);
    print(trueVal || falseVal);

## 赋值运算符

    // = :赋值给变量
    int a = 10;

    // ??= :当变量值为null，则赋值，否则不赋值
    int b;
    b ??= 20;
    print(b); // 值为 20

    int c = 15;
    c ??= 20;
    print(c); // 值为 15

## 条件表达式

    // 三目运算
    int max = 1;
    String size = max == 1 ? "max" : "min";
    print(size);

    // 空判断运算
    String str1;
    String str2 = "dart";
    // str1 若为空，则 str3 值为 str2；str1 不为空，则值为 str1
    String str3 = str1 ?? str2;
    print(str3);

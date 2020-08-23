# 条件控制

## if 语句

    // if 判断
    var number = 1;
    var isMax = true;
    if (number > 0) {
      isMax = true;
    } else {
      isMax = false;
    }

## for 语句

    // for 循环
    var list = [0, "val1", "val2", true, false];
    for (var index = 0; index < list.length; index++) {
      print(list[index]);
    }
    for (var item in list) {
      print(item);
    }

## while 语句

    // while 循环
    var index = 0;
    while (index < 5) {
      index++;
      print(index);
    }
    do {
      index--;
      print(index);
    } while (index > 0);

## break 和 continue

    // break 和 continue
    var list2 = [0, "val1", "val2", true, false];
    for (var index = 0; index < list2.length; index++) {
      if (index == 1) {
        // 跳出当前循环体
        break;
      }
      print(list[index]);
    }
    for (var index = 0; index < list2.length; index++) {
      if (index == 1) {
        // 跳出本次循环条件，继续执行其余循环
        continue;
      }
      print(list[index]);
    }

## switch case 语句

    // switch case 语句
    // 比较类型：num，String，编译器常量，对象，枚举
    var name = "Dart";
    switch (name) {
      case "Dart":
        print("It is Dart");
        break;
      case "Java":
        print("It is Java");
        break;
      default:
        print("It is None");
        break;
    }

    // 使用 continue 跳转标签
    switch (name) {
      Test1: // 给分支添加标签
      case "Dart":
        print("It is Dart");
        // 跳转到指定标签；会执行标签的分支
        continue Test3;
      Test2:
      case "Java":
        print("It is Java");
        break;
      Test3:
      default:
        print("It is None");
        break;
    }

---
layout: post
title: 使用MATLAB进行面向对象编程
date: 2021-07-06
author: zxl19
tags: [MATLAB, Note]
comments: true
toc: true
pinned: false
---

使用MATLAB进行面向对象编程（Object-Oriented Programming，OOP）。

<!-- more -->

## 类的定义

### MATLAB自带的类模板

```matlab
classdef MyClass
    %MYCLASS 此处显示有关此类的摘要
    %   此处显示详细说明

    properties
        Property1
    end

    methods
        function obj = MyClass(inputArg1,inputArg2)
            %MYCLASS 构造此类的实例
            %   此处显示详细说明
            obj.Property1 = inputArg1 + inputArg2;
        end

        function outputArg = method1(obj,inputArg)
            %METHOD1 此处显示有关此方法的摘要
            %   此处显示详细说明
            outputArg = obj.Property1 + inputArg;
        end
    end
end
```

### 示例类实现

```matlab
classdef (Attributes) ClassName < SuperclassName
    properties (Attributes)
        PropertyName
        PropertyName size class {validation functions}
    end
    methods (Attributes)
        function obj = methodName(obj,arg2,...)
            ...
        end
    end
    events (Attributes)
        EventName
    end
end

classdef (Attributes) ClassName < SuperclassName
    enumeration
        EnumName
    end
end
```

### 说明

1. 类文件以`classdef`关键词开始，以`end`结束；
2. 类中包含变量（`properties`）、方法（`methods`）、事件（`events`）和枚举（`enumeration`），以`end`结束；
3. 类文件中可在类声明后定义只在类中使用的函数；
4. 可直接使用模板新建类文件；
5. 类中的函数可定义在外部文件中，但是要和类文件放到同一文件夹中，文件夹名为`@`+`类名`；
6. 类成员名可按`Tab`自动补全；
7. 变量的属性（`Attributes`）默认`public`，可给默认初值；
8. 属性包括：`GetAccess`、`SetAccess`、`Constant`，其中`Constant`可用类名直接调用，无需创建对象；
9. 可有多个变量代码块，对应不同属性；
10. 方法包括构造函数（可选），与类文件同名，在构造对象时调用进行初始化，返回`obj`；
11. 定义`get`和`set`方法，在特定变量被访问时调用：e.g. 输入值合法性判断；
12. 方法的属性也可定义，`Static`属性方法，可用类名直接调用，无需创建对象；
13. 可重载函数、运算符：e.g. `plot`、`subsref`、`subsasgn`；
14. 使用`<`从父类继承，实现代码复用，多个父类间用`&`连接；
15. 继承`handle`类，通过传递句柄（相当于传递引用）减少值传递和拷贝，e.g. `reset`；
16. 构建`delete`方法，相当于析构函数；
17. 通过对`handle`类定义事件来监督对象和变量的变化，调用`addlistener`函数构建`listener`，通过`notify`函数触发事件，`listener`接收触发后执行预先定义的回调函数（`Callback`）；
18. 被监督变化的变量属性需要为`SetObservable`；
19. 在修改类的定义后已创建的类不会更改，因此需要运行`clear`，重新运行代码；

## 资料

### 书籍

1. [Object-Oriented Programming](https://www.mathworks.com/help/pdf_doc/matlab/matlab_oop.pdf)
2. A Guide to MATLAB Object-Oriented Programming
3. MATLAB面向对象编程——从入门到设计模式
4. [Object Oriented Programming and Classes in MATLAB](http://faculty.ce.berkeley.edu/sanjay/e7/oop.pdf)

### 视频

1. [Developing Classes Overview](https://www.mathworks.com/videos/developing-classes-overview-68982.html)
2. [Object-Oriented Programming in MATLAB 丨 Master Class with Loren Shure](https://www.bilibili.com/video/BV1EA411g71G?p=1)

## 参考

1. [Object-Oriented Programming in MATLAB](https://www.mathworks.com/products/matlab/object-oriented-programming.html)
2. [Introduction to Object-Oriented Programming in MATLAB](https://www.mathworks.com/company/newsletters/articles/introduction-to-object-oriented-programming-in-matlab.html)
3. [Classes-MATLAB Help Center](https://www.mathworks.com/help/matlab/object-oriented-programming.html)
4. [MATLAB面向对象编程是什么样的体验？-知乎](https://www.zhihu.com/question/30858386)

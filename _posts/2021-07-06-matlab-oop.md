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
2. 类中包含数据`properties`、算法`methods`、事件`events`和枚举`enumeration`，以end结束；
3. 类文件中可在类声明后定义只在类中使用的函数；
4. 可直接使用模板构建类；
5. 类中的函数可以单独定义在文件中，但是要和类文件放到同一文件夹中，文件夹名为`@`+`类名`；
6. 类成员名可按`Tab`自动补全；
7. `properties`中属性默认`public`，可以给默认初值；
8. 属性`Constant`、`GetAccess`、`SetAccess`；
9. 可有多个`properties`代码块，对应不同属性；
10. 构造函数（可选），在构造对象时调用进行初始化，返回`obj`；
11. 定义`get`和`set`方法；
12. `Static`方法，可用类名直接调用，不需构建对象；
13. 方法的访问属性也可定义；
14. 重载函数、运算符：e.g. subsref、subsasgn；
15. 使用`<`从基类继承，实现代码复用，多个基类间用`&`连接；
16. 使用`handle`类；
17. `events`；
18. `listeners`；

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

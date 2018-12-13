# 随笔

1. 如果一个移动的游戏对象不具有刚体组件，那么游戏对象的碰撞器就不会随游戏对象移动，而具有刚体组件的游戏对象在移动时，它本身以及它的所有子对象的碰撞器将逐帧更新

2. 在C#中，一个属性访问它就会运行其中的get{}语句

3. 冻结了刚体组件的旋转，但如果isKinematic设置为true，仍然可以手动设置刚体的旋转角度(isKinematic=true表示刚体会被物理系统跟踪，但由于Rigibody.velocity的关系，它不会自动移动）如果启用了isKinematic，则力，碰撞或关节将不再影响刚体，但是可以影响到其他的非运动刚体。

4. Unity中的父类和子类:子类继承父类后 如果需要父类的Update方法则要把自己的Update()方法删掉，否则会执行自己的Update()函数，private 修饰的父类Update()方法子类依然可以调用

5. InvokeRepeating()是Unity内置的一个函数，用于对同一函数进行重复调用。函数第一个参数是一个字符串，表示要调用的函数名称，第二个参数设置首次调用该函数的时间间隔，最后一个参数是之后调用该函数的时间间隔。

6. 球状碰撞器的直径将取变换组件中三个维度的最大值

7. 当一个维度的长度远大于其他维度时，也可以使用胶囊状碰撞器。网格碰撞器可以与物体轮廓相吻合，但运行速度比其他碰撞器要慢很多。在高性能计算机上这可能不是什么问题，但在IOS或Android等移动平台上，网格碰撞器的速度通常会很慢。

8. 当在Unity中导入一个dll文件时报错时，在项目面板中点击dll文件可以看到报错信息，可能是支持的.NET版本不同。在Unity中的File->Build Settings->Player Settings->Other Settings中的Configuration下的Scripting Runtime Version中修改成.NET 4.x 即可。当然也可以在VS中修改类库的.NET版本，在右键选择属性 -> 应用程序，将目标框架改为 .NET Framework 3.5或以下，然后重新生成dll导入。

   ![Unity中修改](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img1.png)

   ![VS中修改](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img2.png)

9. 在Unity中使用Protobuf实现数据转换：

   首先从Github上下载protobuf源码

   [选择csharp的版本]https://github.com/protocolbuffers/protobuf/releases

   解压之后进入工程目录下的csharp/src/下，用VS打开Google.Protobuf.sln，右键Google.Protobuf生成，之后会在Google.Protobuf\bin\Debug\net45目录下生成dll文件(也可能不是net45，取决于项目支持的.NET版本)

   接下来准备编译器，编译器是用来将.proto文件编译成相应语音脚本的工具， 编译器可以直接从GitHub上下载

   [Github上下载proto-3.6.1-win32.zip]https://github.com/protocolbuffers/protobuf/releases

   下载解压后会在bin目录下有protoc.exe

   实现protobuf数据转换：

   1. 编写一个.proto文件(syntax是你下载的proto语法版本,有proto2和proto3，package是包名，在Unity中引用的时候就是该名称，message相当于一个类，1，2，3不代表值，代表参数标签，repeated可以理解为数组)

      ![person.proto](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img3.png)

   2. 在cmd窗口下将刚才的.proto文件编译成.CS文件

      ![命令台截图](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img4.png)

      ![执行命令之后](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img5.png)

      --proto_path 指定要编译的.proto文件路径 （相对路径）
      --csharp_out 输出cs文件路径（相对路径）

      [更多proto语法，命令]: https://developers.google.com/protocol-buffers/docs/proto3

   3. 将上面生成的Google.Protobuf.dll 和 Person.cs文件导入到Unity中并测试

      ![Unity测试脚本](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img6.png)

      ![运行结果](D:\MarkDown/images/%E6%B8%B8%E6%88%8F%E8%AE%BE%E8%AE%A1%E3%80%81%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%BC%80%E5%8F%91%E3%80%81%E5%B0%8F%E7%9F%A5%E8%AF%86%E7%82%B9img7.png)

   [为什么要使用Protobuf见腾讯游戏学院]: https://gameinstitute.qq.com/course/detail/10091

10. 当在vs中创建Web项目时弹出：无法创建虚拟目录，无法读取配置文件，需要在IIS中手动创建此虚拟目录才能打开此项目。的窗口时，是因为此电脑下的IISExpress快捷方式无效，去Documents下删除无效的IISExpress快捷方式即可解决。

11. C#在变量之间有一个基本区分，把类型级别声明的变量看作字段，而把在方法中声明的变量看作局部变量。在类中声明的变量(字段)会被方法中声明的同名局部变量隐藏，所以取得值是局部变量的。

12. 常量是类似 ```const int a =100; ```常量必须在声明时初始化，常量的值必须在编译时用于计算，常量总是静态的(不必包含修饰符```static```，实际上也不允许)

13. 在C#中，“函数成员”不仅包含方法，也包含类或结构的一些非数据成员，如索引器、运算符、构造函数和析构函数等，甚至还有属性(属性与字段的区别:属性是有get,set方法的)，字段、常量和事件才是数据成员

14. 可变参数(params关键字)与可选参数的区别：

    可变参数：

    1. 使用 params关键字可以指定一个方法参数,该方法参数的数目可变。
    2. 可以发送参数声明中所指定类型的逗号分隔的参数列表或指定类型的参数数组。 还可以不发送参数。 如果未发送任何参数，则 params列表的长度为零。
    3. 在方法声明中的 params关键字之后不允许任何其他参数，并且在方法声明中只允许一个 params关键字。

    可选参数：

      1.参数是可选的，但必须为可选参数提供默认值，而且必须是方法定义的最后一个参数。

15. C#重载方法的参数有一些小限制：两个方法不能仅在返回类型上有区别，两个方法不能仅根据参数是声明为```ref```还是```out```来区分

16. as运算符用于执行**引用类型**的显示类型转换，如果要转换的类型与指定的类型兼容，转换就会成功进行，如果不兼容，as运算符就会返回null值

17. 如果对复杂类型(和非基本类型)使用sizeof运算符，就需要把代码放在unsafe块中

    ```unsafe{Console.WriteLine(sizeof(Customer))}```

18. ```typeof```运算符返回一个表示特定类型的```System.Type```对象，如```typeof(string)```返回表示```System.String```类型的Type对象。在使用反射技术动态查找对象的相关信息时很有用。

19. 可空类型如```int? a = null```，但是在比较可空类型时，只要有一个操作数为null，比较结果就是false。**即不能因为一个条件是false，就认为该条件的对立面为true**，例如：

    ```c#
    int? x = null;
    int? y = a + 4;// y = null
    
    int? a = null;
    int? b = -5;
    if(a >= b)
        Console.WriteLine("a >= b");
    else
        Console.WriteLine("a < b");
    ```

20. 空合并运算符```(??)```，可以在处理可空类型和引用类型时表示null可能的值。**这个运算符要放在两个操作数之间，第一个操作数必须是一个可空类型或引用类型；第二个操作数必须与第一个操作数的类型相同，或者可以隐含地转换为第一个操作数的类型。**

    计算规则为：如果第一个操作数不是null，整个表达式就等于第一个操作数的值。如果第一个操作数是null，整个表达式就等于第二个操作数的值。

    ```C#
    int? a = null;
    int b;
    
    b = a ?? 10;//b has the value 10
    a = 3;
    b = a ?? 10;//b has the value 3
    ```

21. 可空类型隐示地转换为其他可空类型，应遵循非可空类型的转换规则，即```int?```隐式地转换为```long?```、```float?```、```double?```、和```decimal?```。

    非可空类型隐式地转换为可空类型也遵循非可空类型的转换规则，即```int?```隐式地转换为```long?```、```float?```、```double?```、和```decimal?```。

    可空类型不能隐式地转换为非可空类型，必须进行显式转换。

22. 拆箱时要确保得到的值变量有足够的空间存储拆箱的值中的所有字节。

23. C#不允许重载“=”，但如果重载“+”运算符，编译器就会自动使用“+”运算符的重载来执行“+=”运算符的操作

24. C#要求成对重载比较运算符，且比较运算符必须返回布尔类型的值。

25. 用户定义的类型强制转换：类似于重载运算符，也必须同时声明```public```和```static```。例：

    ```C#
    //这里的implicit关键字用于声明隐式用户定义的类型转换运算符。如果保证转换不会导致数据丢失，则使用它来启用用户定义类型与其他类型之间的隐式转换。
    //也可以指定explicit关键字，它声明了必须使用强制转换调用的用户定义的类型转换运算符。
    //运算符的返回类型定义了类型强制转换操作的目标类型(float既是目标类型，也是返回类型)
    //如果数据类型转换声明为隐式(implicit)，编译器就可以隐式或显式地使用这个转换，如果数据类型转换声明为显式(explicit)，编译器就只能显式的使用它。
    public static implicit operator float (Currency value){
        
    }
    ```

26. 类之间的类型强制转换：

    1. 如果某个类派生自另一个类，就不能定义这两个类之间的类型强制转换(这些类型的类型转换已经存在)
    2. 类型强制转换必须在源数据类型或目标数据类型的内部定义
    3. 一旦在一个类的内部定义了类型强制转换，就不能在另一个类中定义相同的类型强制转换。

27. 装箱和拆箱数据类型强制转换：不能从结构或基元值类型中派生。所以基本结构和派生结构之间的强制转换总是基元类型或结构与```System.Object```之间的转换(理论上可以在结构和```System.ValueType```之间进行强制转换，但一般很少这么做)

    ```C#
    object derivedObject = new Currency(40,0);
    object baseObject = new object();
    Currency derivedCopy1 = (Currency)derivedObject;// OK
    Currency derivedCopy2 = (Currency)baseObject;	//Exception thrown
    //第一种可以成功，第二种会失败，因为baseObject没有引用已装箱的Currency对象
    ```

28. .NET MVC下使用```$.ajax({})```访问```Controller```不能通过```Return RedirectToAction(ActionName,ControllerName)```来跳转**视图(View)**，它所返回的将是对应```Action```返回```View```的```text(在浏览器F12下可以打印返回的信息，发现是一个Html页面的源码)```，不能真正的跳转到对应的界面，但是可以通过返回对应```View```或者```Controller```的```Url```在```ajax```的```success```方法中使用```window.locaion.href```来进行跳转。而form表单的Action以及Razor中的```@Html.BeginForm```是可以在Controller实现跳转```View```的。

29. 跳转页面一般不传递集合或一个对象而是一个ID或者简单的数据，因为传递集合时如果数据库中的数据修改了，这个集合传的数据就是错误的，还可能网络带宽的问题，要节省带宽。所以一般传递一个ID之后再在对应的视图再查询一遍这个对象。


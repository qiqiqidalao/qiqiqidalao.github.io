# 随笔

1. 如果一个移动的游戏对象不具有刚体组件，那么游戏对象的碰撞器就不会随游戏对象移动，而具有刚体组件的游戏对象在移动时，它本身以及它的所有子对象的碰撞器将逐帧更新

2. 在C#中，一个属性访问它就会运行其中的get{}语句

3. 冻结了刚体组件的旋转，但如果isKinematic设置为true，仍然可以手动设置刚体的旋转角度(isKinematic=true表示刚体会被物理系统跟踪，但由于Rigibody.velocity的关系，它不会自动移动）如果启用了isKinematic，则力，碰撞或关节将不再影响刚体，但是可以影响到其他的非运动刚体。

4. Unity中的父类和子类:子类继承父类后 如果需要父类的Update方法则要把自己的Update()方法删掉，否则会执行自己的Update()函数，private 修饰的父类Update()方法子类依然可以调用

5. InvokeRepeating()是Unity内置的一个函数，用于对同一函数进行重复调用。函数第一个参数是一个字符串，表示要调用的函数名称，第二个参数设置首次调用该函数的时间间隔，最后一个参数是之后调用该函数的时间间隔。

6. 球状碰撞器的直径将取变换组件中三个维度的最大值

7. 当一个维度的长度远大于其他维度时，也可以使用胶囊状碰撞器。网格碰撞器可以与物体轮廓相吻合，但运行速度比其他碰撞器要慢很多。在高性能计算机上这可能不是什么问题，但在IOS或Android等移动平台上，网格碰撞器的速度通常会很慢。

8. 当在Unity中导入一个dll文件时报错时，在项目面板中点击dll文件可以看到报错信息，可能是支持的.NET版本不同。在Unity中的File->Build Settings->Player Settings->Other Settings中的Configuration下的Scripting Runtime Version中修改成.NET 4.x 即可。当然也可以在VS中修改类库的.NET版本，在右键选择属性 -> 应用程序，将目标框架改为 .NET Framework 3.5或以下，然后重新生成dll导入。

   ![Unity中修改](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img1.png)

   ![VS中修改](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img2.png)

9. 在Unity中使用Protobuf实现数据转换：

   首先从Github上下载protobuf源码

   [选择csharp的版本]https://github.com/protocolbuffers/protobuf/releases

   解压之后进入工程目录下的csharp/src/下，用VS打开Google.Protobuf.sln，右键Google.Protobuf生成，之后会在Google.Protobuf\bin\Debug\net45目录下生成dll文件(也可能不是net45，取决于项目支持的.NET版本)

   接下来准备编译器，编译器是用来将.proto文件编译成相应语音脚本的工具， 编译器可以直接从GitHub上下载

   [Github上下载proto-3.6.1-win32.zip]https://github.com/protocolbuffers/protobuf/releases

   下载解压后会在bin目录下有protoc.exe

   实现protobuf数据转换：

   1. 编写一个.proto文件(syntax是你下载的proto语法版本,有proto2和proto3，package是包名，在Unity中引用的时候就是该名称，message相当于一个类，1，2，3不代表值，代表参数标签，repeated可以理解为数组)

      ![person.proto](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img3.png)

   2. 在cmd窗口下将刚才的.proto文件编译成.CS文件

      ![命令台截图](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img4.png)

      ![执行命令之后](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img5.png)

      --proto_path 指定要编译的.proto文件路径 （相对路径）
      --csharp_out 输出cs文件路径（相对路径）

      [更多proto语法，命令]: https://developers.google.com/protocol-buffers/docs/proto3

   3. 将上面生成的Google.Protobuf.dll 和 Person.cs文件导入到Unity中并测试

      ![Unity测试脚本](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img6.png)

      ![运行结果](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img7.png)

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

30. C#中的Interface中接口声明默认是public的，所以不能对接口中的抽象方法或属性使用public关键字，同时接口中不能声明**字段**但是可以声明**属性**，接口成员不能有 new、static、abstract、override、virtual 修饰符。有一点要注意，当一个接口实现一个接口，这2个接口中有相同的方法时，可用 new 关键字隐藏父接口中的方法。**接口中只能包含方法、属性、事件和索引的组合**。

31. 索引器是一种语法上的遍历，最常见以类型实现，其主要目的是封装内部集合或数组。例如：假设有一个TempRecord表示Farenheit温度的类，在24小时内以10个不同的时间记录。该类包含一个用于存储温度值temps的类型数组float[]。通过在此类中实现索引器，客户端可以访问TempRecord实例中的温度```float temp = tr[4]```而不是```float temp = tr.temps[4]```。索引器表示法不仅简化了客户端应用程序的语法; 它还使该类及其目的更直观，供其他开发人员理解。**要在类或结构上声明索引器，要使用this关键字：```public int this[index]{   //get and set 访问器}```

32. C#中的委托和事件，事件可以理解为类似声明一个进行了封装的委托类型的变量，但在类的内部，不管你用public修饰event还是用protected修饰event，它总是private，在声明委托的时候不能使用static关键字，而声明委托和声明类型类似，可以在后面创建委托变量的时候像类型一样使用。下面代码块第二行和第十行。

    ```C#
     	//委托类型
        public delegate void TestDelegate();
        delegate void CustomizeEvent(NotImpEventArgsClass e);
    	//加泛型则不会在使用系统的EvnetHandler<TEventArgs>
        public delegate void EventHandler();
    
        class Program
        {
            //委托变量
            public static TestDelegate testDelegate;
            //自定义事件
            public static event TestDelegate TestEvent;
            public static event CustomizeEvent ce;
            public static event EventHandler ee;
            //符合.NET FrameWork编码规范的事件，这里的EventArgs可以是任意其它类型
            //这里的泛型类型作用就是存储事件要处理的数据类
            //系统的EventHandler<TEventArgs>定义为： 
            //public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e);
            //也可以不使用系统的EventHandler<TEventArgs>，可以自己写一个EventHandler<T>，但是在当前类中就会使用自己写的EventHandler<T>，如果没有写成EventHandler<T>而是EventHandler则不会影响。
            private static EventHandler<EventArgs> newEvent;
            //写成属性类似的方式就不能使用NewEvent(sender,e)这种，只能使用它对应的字段newEvent
            public static event EventHandler<EventArgs> NewEvent
            {
                add { newEvent += value; }
                remove { newEvent -= value; }
            }
            public static event EventHandler<EventArgs> Another;
    
            static void Main(string[] args)
            {
                testDelegate += Function;
                testDelegate();
    
                TestEvent += Function1;
                TestEvent();
    
                NewEvent += Function2;
                Another += Function2;
    
                //.NET FrameWork自带的泛型委托EventHandler<TEventArgs>要求传递两个参数
                //第一个参数为object类型,第二个参数为泛型TEventArgs
                newEvent(newEvent, new TestEventArgs());
                Another(Another.GetType(), new EventArgs());
    
                ce += Function3;
                ce(new NotImpEventArgsClass());
    
                ee += Function1;
                
                Console.ReadLine();
            }
    
            public static void Function()
            {
                Console.WriteLine("Function 自定义委托");
            }
    
            public static void Function1()
            {
                Console.WriteLine("Function1 使用自定义事件");
            }
    
            public static void Function2(object sender,EventArgs e)
            {
                Console.WriteLine("Function2 使用.NET规范的事件");
            }
    
            public static void Function3(NotImpEventArgsClass customize)
            {
                Console.WriteLine("Function3 使用自定义事件");
            }
        }
    
        class NotImpEventArgsClass
        {
    
        }
    
        class TestEventArgs : EventArgs
        {
    
        }
    ```

33. 在Linux上装好```redis```之后要去```redis.conf```中修改```daemonize``` 为```yes```(在vim编辑器中敲/进入查询模式，敲n查找下一个，N查找上一个)，```redis server```就可以后台启动了，启动```redis```服务可以在```redis-server```可执行文件目录下(一般在```src```目录下)输入```./redis-server ../redis.conf```(要使用配置文件启动)，启动之后就可以使用```./redis-cli```进入了，使用```./redis-cli SHUTDOWN```关闭```redis-server```

    ![运行结果](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img8.png)

34. 不是所有查询都可以用LINQ查询语法完成，也不是所有的扩展方法都映射到LINQ查询子句上。高级查询要使用扩展方法。不能使用LINQ查询的一个例子是Where()方法的重载，在Where方法的重载中，可以传递第二个参数——索引。该索引是被执行查询的集合的索引。可以在表达式中使用这个索引，执行基于索引的计算

    ```C#
    List<Person> people = new List<Person> {
    	new Person { Name = "张三", Age = 29 },
    	new Person { Name = "李四", Age = 39 },
    	new Person { Name = "王五", Age = 22 },
    	new Person { Name = "王二", Age = 29 }
    };
    //两种写法的效果一样
    var useLinq = from p in people
    	where p.Age < 30
    	select p.Name;
    var useExtendMethod = people.Where(p => p.Age < 30).Select(p => p.Name);
    //Where的重载方法，筛选年龄小于30且索引为偶数的人，索引index是people集合中的索引，不是筛选后的索引
    var res = people.Where((p, index) => p.Age < 30 && index % 2 == 0).Select(p => p.Name);
    
    //基于类型筛选
    object[] data = { "one", 1, 2, "flour", 'c' };
    var query = data.OfType<int>();
    
    //SelectMany例子
    PetOwner[] petOwners = {
    	new PetOwner { Name="Higa",Pets = new List<string>{ "Scruffy", "Sam" } },
    	new PetOwner { Name="Ashkenazi",Pets = new List<string>{ "Walker", "Sugar" } },
    	new PetOwner { Name="Price",Pets = new List<string>{ "Scratches", "Diesel" } },
    	new PetOwner { Name="Hines",Pets = new List<string>{ "Dusty" } }
    };
    //SelectMany扩展方法：
    //public static IEnumerable<TResult> SelectMany<TSource, TCollection, TResult>
    //(this IEnumerable<TSource> source, 
    //Func<TSource, IEnumerable<TCollection>> collectionSelector, 
    //Func<TSource, TCollection, TResult> resultSelector);
    //第一个参数就是传递进去的集合(写的时候不用写出来，直接从第二个参数开始)，
    //第二个是对该集合要进行操作的转换函数形成中间集合，
    //第三个是对中间集合的每个元素的转换函数。
    //根据扩展方法的定义，第二个参数的方法一定要传TSource类型，并且会返回一个集合类型，第三个参数一定要传递两个参数的方法，并且返回一个转换后的集合。
    //这里也可以不使用lambda表达式，可以传递方法 只要符合委托的签名即可(未测试)
    var query = petOwners
    	.SelectMany(petOwner => petOwner.Pets, (petOwner, petName) => new { petOwner, petName })
    	.Select(ownerAndPet => new
    		{
    			Owner = ownerAndPet.petOwner.Name,
    			Pet = ownerAndPet.petName
    		}
    	);
    //复合LINQ子句实现SelectMany()效果
    var query = from p in petOwners
                from pets in p.Pets
                select new { p.Name, pets };
    //执行的结果为
    //{ Owner = Higa, Pet = Scruffy }
    //{ Owner = Higa, Pet = Sam }
    //{ Owner = Ashkenazi, Pet = Walker }
    //{ Owner = Ashkenazi, Pet = Sugar }
    //{ Owner = Price, Pet = Scratches }
    //{ Owner = Price, Pet = Diesel }
    //{ Owner = Hines, Pet = Dusty }
    
    //GroupBy分组
    List<int> numbers = new List<int> { 1, 2, 3, 2, 2, 3, 1, 3, 2, 4, 2, 3, 4, 5, 1, 2 };
    //LINQ方式
    var query = from i in numbers
                group i by i into g
                select g;
    //使用GroupBy扩展方法
    query = numbers.GroupBy(i => i);
    //使用ToLookUp扩展方法
    query = numbers.ToLookup(i => i);
    //GroupBy和ToLookup效果类似，但是GroupBy会延迟执行
    //当你遍历集合的时候,下一个要出现的项目可能会或者可能不会被加载
    //它实际上是在第一项被使用的时候创建分组,而不是在 GroupBy（） 第一次被调用时
    //使用ToLookUp时，LookUp集合是不可改变的，一旦创建就不能删除或添加元素
    List<int> numbers = new List<int> { 1, 2, 3, 2, 2, 3, 1, 3, 2, 4, 2, 3, 4, 5, 1, 2 };
    var query = numbers.GroupBy(i => i);
    //var query = numbers.ToLookup(i => i);
    numbers.RemoveAll(i => i == 1);
    foreach (var i in query)
    	Console.WriteLine("i.Key: " + i.Key + " i.Count(): " + i.Count());
    //使用GroupBy结果
    //i.Key: 2 i.Count(): 6
    //i.Key: 3 i.Count(): 4
    //i.Key: 4 i.Count(): 2
    //i.Key: 5 i.Count(): 1
    //使用ToLookUp结果
    //i.Key: 1 i.Count(): 3
    //i.Key: 2 i.Count(): 6
    //i.Key: 3 i.Count(): 4
    //i.Key: 4 i.Count(): 2
    //i.Key: 5 i.Count(): 1
    ```

35. 与```var```关键字不同，定义为```dynamic```的对象可以在运行期间改变其类型。注意在使用```var```关键字时，对象类型的确定会延迟。类型一旦确定，就不能改变。动态对象的类型可以改变，而且可以改变多次，这不同于把对象的类型强制转换为另一种类型。在强制转换对象的类型时，是用另一种兼容的类型创建一个新对象。**```dynamic```类型有两个限制，动态对象不支持扩展方法，匿名函数(lambda表达式)也不能用作动态方法调用的参数，因此LINQ不能用于动态对象。**

    ```C#
    dynamic a = 5;
    Console.WriteLine(a.GetType());
    a = "Hello";
    Console.WriteLine(a.GetType());
    a = new Student { Name = "小王", Id = 5 };
    Console.WriteLine(a.Name);
    //输出结果
    //System.Int32
    //System.String
    //小王
    ```

36. 可以使用```await```关键字来调用返回任务的异步方法，使用```await```关键字需要有用```async```修饰符声明的方法，在异步方法完成前，该方法内的其他代码不会继续执行。但是，启动调用异步方法的方法(即用```async```)修饰的方法的线程可以被重用，该线程没有被阻塞。

37. ```async```修饰符只能用于返回Task或void的方法，它不能用于程序的入口点，即Main方法不能使用```async```修饰符，await只能用于返回Task的方法。

38. Task类的```ContinueWith```方法定义了任务完成后就调用的代码。指派给```ContinueWith```方法的委托接收将已完成的任务作为参数传入，使用Result属性可以访问任务返回的结果

    ```C#
    static string Greeting(string name)
    {
    	Thread.Sleep(3000);
    	return string.Format("Hello, {0}", name);
    }
    
    static Task<string> GreetingAsync(string name)
    {
    	return Task.Run<string>(() => { return Greeting(name); });
    }
    
    private async static void CallerWithAsync()
    {
    	string result = await GreetingAsync("Stephanie");
    	Console.WriteLine(result);
    }
    //该方法没有指定async关键字，所以调用ContinueWith时并不会等待，该方法还是会继续执行
    //若要等待执行完在往下执行，该方法要加async关键字，并在ContinueWith之前使用await关键字
    private static void CallerWithContinuationTask()
    {
    	Task<string> t1 = GreetingAsync("Stephanie");
    	t1.ContinueWith(t =>
    	{
    		string result = t.Result;
    		Console.WriteLine(result);
        });
        Console.WriteLine(1);
    }
    ```

39. Task组合器接受多个Task对象作为参数，并返回一个Task。如果多个Task对象的类型相同，则返回同一类型值，再加上await关键字，则会进一步获得结果数组(比如参数都是```Task<string>```，不用await则返回类型是```Task<string>```，使用await关键字之后则是```string[]```类型)，如果多个Task对象的类型不相同，也可以返回一个Task，但用await会返回void类型。

    ```C#
    private static async void UseTaskWhenAll()
    {
    	Task<string> t1 = GreetingAsync("Stephanie");
    	Task<string> t2 = GreetingAsync("Matthias");
    	Task t3 = Task.Run(() => Console.Write("3"));
    	await Task.WhenAll(t1, t2, t3);//等待任务返回 无值
    	Task t4 = Task.WhenAll(t1, t2, t3);//返回一个Task
    	string[] res = await Task.WhenAll(t1, t2);//返回一个string[]
    }
    ```

40. 栈是从上而下分配空间，即由高内存地址指向低内存地址填充，而堆是从下而上分配空间。编译器遇到```int i,j```这样的代码行，则这两个变量进入作用域的顺序是不确定的。两个变量是同时声明的，也是同时超出作用域的。内部会确保先放在内存的后删除。声明一个引用类型时，先给引用变量在**栈**上分配存储空间，但这仅仅是一个引用，而不是实际的对象，只有再new了之后才会分配堆上的内存，以存储对象，然后把引用变量的值设置为该对象的内存地址。

41. 当一个引用变量超出作用域时，就会从栈中删除，但引用对象的数据仍保留在堆中，直到程序终止，或垃圾回收器删除它为止，而只有在该数据不再被任何变量引用时，它才会被删除。

42. 使用```SQLyog```可视化工具连接```MySQL```时出现```plugin caching sha2 password could not be loaded```问题(不局限于用```SQLyog```连接，其它可视化工具可能也有这个问题)，原因是从mysql8开始使用的加密方式为：```caching-sha2-password```，而可视化工具能识别的加密方式还是原来的:```mysql_native_password```，因此需要把mysql8的root用户密码加密方式改为```mysql_native_password```

    ```sql
    #更新root用户的密码为1234
    #只会改变root用户的密码加密方式，其他用户的密码加密方式不影响
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '1234';
    #刷新权限
    FLUSH PRIVILEGES;
    ```

43. C#中的数组实际上都是对象，它们都是```System.Array```的实例。因此数组存储在堆上。可以使用```stackalloc```，命令指示.NET运行库在栈上分配一定的内存，在使用```stackalloc```命令时，需要为它提供两条信息：要存储的数据类型、需要存储的数据项数。```stackalloc```后面紧跟要存储的数据类型名(该数据类型必须是一个值类型)

    ```C#
    //不能是decimal[] pDecimals = stackalloc decimal[10];
    //因为stackalloc总是返回分配数据类型的指针
    //但是这种方式分配的数组，如果使用pDecimals[20] = 2.0;编译器不会报错
    decimal* pDecimals = stackalloc decimal[10];
    ```

44. 使用``` MySqlTransaction tran = conn.BeginTransaction();```之后就开始事务了，然后为```SqlCommand```对象设置```Transaction```对象，接着事务处理，最后提交或者回滚，如果使用了```BeginTransaaction```之后并没有提交，则数据库中并不会更新。```MySqlTransaction```对象是针对连接的，而不是针对SQL命令的，所以即使不写```comm.Transaction = tran```，只要最后有```tran.Commit();```还是会对数据库进行更新

45. ```IEnumerable```适用于只遍历集合的时候，它只能以只读的方式访问集合，不能用于修改，它只有一个```GetEnumerator```方法用于返回一个迭代器。```ICollection```继承了```IEnumerable```接口，同时拥有三个属性和一个方法，```Count```：获取```ICollection```中包含的元素数，```IsSynchronized```：获取一个值，该值指示是否同步对```ICollection```的访问（线程安全）。```SyncRoot```：获取一个对象，该对象可用于同步对```ICollection```的访问，```CopyTo(Array, Int32)```：从特定的```Array```索引开始，将```ICollection```的元素复制到```Array```。```IList```则继承了```ICollection、IEnumerable```接口，并新增了更多的属性和方法，可以对集合进行增删等操作。

46. 在```Unity```中使用```Camera.main```时，应当注意是否有摄像机的```Tag```标签为```MainCamera```，否则会报空指针异常，当然也可以使用```GameObject.Find(摄像机名称)```来获取摄像机再继续使用。

47. ```Input.GetMouseButtonDown```在用户按下给定鼠标按钮的帧期间返回```true```。需要从```Update```函数调用此函数，**因为每个帧都会重置状态。**在用户释放鼠标按钮并再次按下鼠标按钮之前，它不会返回```true```。 主按钮（通常是左按钮）的*按钮*值为0，辅助按钮的按钮值为1，中间按钮的*按钮*值为2。

48. 在老版本的Unity中(4.X或者5.X)中，```foreach```会发生装箱拆箱操作，但是在新的版本中，Unity已经优化了，不会发生装箱拆箱，但是依然有```GC alloc```的操作(即产生了```GC```)。

49. Serialize的功能：可以将成员变量在Inspector面板中显示，并且定义Serialize关系，简单的说，在Inspector面板中可见的值都会被保存成二进制文件。

50. ```[SerializeField]```这个特性会强制Unity序列化**私有字段**并在Inspector面板中显示，可序列化的类型：

    - 所有继承自```UnityEngine.Object```的类，例如```GameObject，Component，MonoBehaviour，Texture2D，AnimationClip```
    - 所有基本数据类型，如```int，string，float，bool```
    - 一些内置类型，如```Vector2，Vector3，Vector4，Quaternion，Matrix4x4，Color，Rect，LayerMask```
    - 可序列化类型的数组
    - 可序列化类型的列表
    - 枚举
    - 结构

51. ```[Serializable]```这个特性允许在Inspector面板中显示**自定义的类或结构**，需要在声明类的时候声明特性，然后声明类型变量的时候才会在Inspector面板中显示：

    ```c#
    [Serializable]
    public class Type2
    {
    	public int p = 5;
    	public Color c = Color.white;
    }
    
    public Type2 myType2;
    ```

52. ```EditorGUILayout.TextField```和```EditorGUILayout.TextArea```的区别：```TextField```创建一个单行文本字段，用户可以在其中编辑字符串。而```TextArea```创建一个多行文本字段，用户可以在其中编辑字符串。即```TextArea```中可以换行输入，但是注意换行输入的字符串```TextField```只能显示第一行。

    ![](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img9.png)

    ![](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img10.png)

53. ```transform.forward```与```Vector3.forward```的不同：```transform.forward```操作```GameObject```在**世界空间**中变换的Z轴上的位置，而```Vector3.forward```就是```Vector3(0, 0, 1)```的简写(一般用于**自身坐标系**)，所以在控制角色往前移动时可以用两种方式:

    ```C#
    //Translate第二个参数不指定，则默认为Space.Self
    transform.Translate(Vector3.forward * speed * Time.deltaTime);
    
    transform.Translate(transform.forward * speed * Time.deltaTime, Space.World);
    
    transform.Translate(transform.rotation * Vector3.forward * speed * Time.deltaTime, Space.World);
    ```

    ```transform.rotation * Vector3.forward  ==  transform.forward```

    一个四元数乘以一个方向向量的意思是将这个方向向量旋转这个旋转(指四元数代表的旋转)

    注意：四元数和向量相乘一定是左乘(即四元数必选在左侧)

54. 如果Unity打开C# Project时，在VS中无法打开项目属性面板，解决办法是在工具->选项->适用于Unity的工具->常规->杂项->访问项目属性设置为True，重启VS，Unity即可

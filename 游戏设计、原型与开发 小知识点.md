###  游戏设计、原型与开发 小知识点

1. 如果一个移动的游戏对象不具有刚体组件，那么游戏对象的碰撞器就不会随游戏对象移动，而具有刚体组件的游戏对象在移动时，它本身以及它的所有子对象的碰撞器将逐帧更新

2. 在C#中，一个属性访问它就会运行其中的get{}语句

3. 冻结了刚体组件的旋转，但如果isKinematic设置为true，仍然可以手动设置刚体的旋转角度(isKinematic=true表示刚体会被物理系统跟踪，但由于Rigibody.velocity的关系，它不会自动移动）

4. Unity中的父类和子类:子类继承父类后 如果需要父类的Update方法则要把自己的Update()方法删掉，否则会执行自己的Update()函数，private 修饰的父类Update()方法子类依然可以调用

5. InvokeRepeating()是Unity内置的一个函数，用于对同一函数进行重复调用。函数第一个参数是一个字符串，表示要调用的函数名称，第二个参数设置首次调用该函数的时间间隔，最后一个参数是之后调用该函数的时间间隔。

6. 球状碰撞器的直径将取变换组件中三个维度的最大值

7. 当一个维度的长度远大于其他维度时，也可以使用胶囊状碰撞器。网格碰撞器可以与物体轮廓相吻合，但运行速度比其他碰撞器要慢很多。在高性能计算机上这可能不是什么问题，但在IOS或Android等移动平台上，网格碰撞器的速度通常会很慢。

8. 当在Unity中导入一个dll文件时报错时，在项目面板中点击dll文件可以看到报错信息，可能是支持的.NET版本不同。在Unity中的File->Build Settings->Player Settings->Other Settings中的Configuration下的Scripting Runtime Version中修改成.NET 4.x 即可。当然也可以在VS中修改类库的.NET版本，在右键选择属性 -> 应用程序，将目标框架改为 .NET Framework 3.5或以下，然后重新生成dll导入。

   ![](D:\Markdown\images\游戏设计、原型与开发、小知识点img1.png)

   ![](D:\Markdown\images\游戏设计、原型与开发、小知识点img2.png)

9. 在Unity中使用Protobuf实现数据转换：

   首先从Github上下载protobuf源码

   [选择csharp的]:https://github.com/protocolbuffers/protobuf/releases

   解压之后进入工程目录下的csharp/src/下，用VS打开Google.Protobuf.sln，右键Google.Protobuf生成，之后会在Google.Protobuf\bin\Debug\net45目录下生成dll文件(也可能不是net45，取决于项目支持的.NET版本)

   接下来准备编译器，编译器是用来将.proto文件编译成相应语音脚本的工具， 编译器可以直接从GitHub上下载

   [Github上下载proto-3.6.1-win32.zip]:https://github.com/protocolbuffers/protobuf/releases

   下载解压后会在bin目录下有protoc.exe

   实现protobuf数据转换：

   1. 编写一个.proto文件(syntax是你下载的proto语法版本,有proto2和proto3，package是包名，在Unity中引用的时候就是该名称，message相当于一个类，1，2，3不代表值，代表参数标签，repeated可以理解为数组)

      ![person.proto](D:\Markdown\images\游戏设计、原型与开发、小知识点img3.png)

   2. 在cmd窗口下将刚才的.proto文件编译成.CS文件

      ![](D:\Markdown\images\游戏设计、原型与开发、小知识点img4.png)

      ![](D:\Markdown\images\游戏设计、原型与开发、小知识点img5.png)

      --proto_path 指定要编译的.proto文件路径 （相对路径）
      --csharp_out 输出cs文件路径（相对路径）

      [更多proto语法，命令]:https://developers.google.com/protocol-buffers/docs/proto3

   3. 将上面生成的Google.Protobuf.dll 和 Person.cs文件导入到Unity中并测试

      ![](D:\Markdown\images\游戏设计、原型与开发、小知识点img6.png)

      ![](D:\Markdown\images\游戏设计、原型与开发、小知识点img7.png)

   [为什么要使用Protobuf见腾讯游戏学院]:https://gameinstitute.qq.com/course/detail/10091

10. 


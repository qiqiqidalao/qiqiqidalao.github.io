使用Unity自带的Network Manager组件和Network Manager HUD组件，Network Manager 组件管理网络游戏物体的状态，Network Manager HUD获取一个简单的UI界面控制连接等等。LAN Host既是服务器也是客户端，LAN Client需要指定连接服务器的IP和端口，LAN Server则是只作为服务器。

为了识别玩家的GamgObject，需要在玩家物体上添加Network Identity组件，主要是辨别是否需要被网络系统需要，Server Only参数表示这个物体由服务器控制，Local Player Authority表示由本地玩家控制

控制玩家的脚本需要继承自NetworkBehaviour而不是MonoBehaviour，在NetworkBehaviour中暴露了一个isLocalPlayer参数来判断玩家是否是本地玩家，通过isLocalPlayer的判断玩家只能控制自己的角色，而不同的客户端之间位置、旋转等同步需要在玩家的预制体上增加Network Transform组件。

Network Transform中有一个Network Send Rate参数，控制向服务器发送的评率，不能过高也不能过低。过低会造成同步看上去有点卡顿，过高会导致发送的数据过多，可能在移动端上的效果不好。

NetworkBehaviour有一个OnStartLocalPlayer()函数，这个函数只会被本地的客户端中调用。

使用这种Untiy自带的网络组件时，在服务器和客户端共享脚本的情况下，有一种控制逻辑流的方式就是使用isLocalPlayer标志位，另一种方式则是使用Command特性，Command特性表示定义的函数是在客户端调用但是在服务器上执行，函数任何参数都会通过Command传给服务器。Command只能从本地的玩家对象发送出去，Command特性修饰的函数也必须以Cmd开头。

通过调用NetworkServer.Spawn(需要生成的对象)，可以在每个客户端生成这个对象，并且这个对象由服务器管理，这个对象销毁，则所有的客户端也会销毁这个对象，即由服务器同步这个对象。

使用这种Untiy自带的网络组件时，要网络同步某个属性的时候，需要使用SyncVar特性，并且需要使用hook绑定一个函数，且这个函数需要有和修饰的属性同类型的形参

![](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/15.png)

还可以使用ClientRpc特性，ClientRpc修饰的函数将在服务器上调用，在客户端上执行，与Command相反。且ClientRpc修饰的函数需要以Rpc开头。

Input.GetAxis("Horizontal") * Time.deltaTime * 150.0f (这里的150.0f相当于角速度，因为获取的是水平方向)

Input.GetAxis("Vertical") * Time.deltaTime * 3.0f (这里的3.0f相当于前进速度，因为获取的是垂直方向)


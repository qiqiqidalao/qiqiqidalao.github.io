1. 标准着色器(Standard)主要是针对硬质表面设计，可以处理现实世界中的大多数材质，比如石头、陶瓷、铜器、银器或橡胶，皮肤、头发等。其中Standard的Albedo属性是物体表面的基本颜色，在物理模型中相当于表面的散射颜色。可以点击该属性名前方的圆圈选择贴图，也可以通过后方的方框选择颜色。Metallic属性是物体表面对光线反射的能量，通常金属物体超过50%，大部分在90%，而非金属物体则击中在20%以下。Smoonthness属性值越大，物体越光滑，反之越粗糙。normal map属性是物体的法线贴图。Emission属性表示物体是否自发光。

2. AudioSource组件中的Bypass Effects属性表示是否打开音频特效，Pitch属性表示播放速度(取值范围在-3到3之间。设置1为正常播放，小于1为减慢播放，大于1为加速播放)。

3. GUI.Button绘制按钮，常与if语句配合使用，有两个参数，第一个参数为按钮的位置和大小，第二个参数为按钮的文本。GUI.Label绘制文本，GUI.DrawTexture绘制贴图，GUI.Box绘制一个图形框，GUI.Window绘制一个窗口，GUI.TextField绘制输入框，GUI.PasswordField绘制密码输入框，GUI.HorizontalScrollBar绘制水平滚动条。

4. Mathf.Sin以及Mathf.Cos使用弧度作为单位，因此传入角度时需要使用"弧度 = 角度 * 2π / 360"将角度转换成弧度

5. 锁视角的相机跟随可以根据跟随目标的位置，并指定好纵向角度以及横向角度，通过三角函数的使用将摄像机的位置锁定跟随

   ```c#
   //rot为横向角度，roll为纵向角度
   Vector3 targetPos = target.transform.position;
   
   Vector3 cameraPos = Vector3.zero;
   
   float d = distance * Mathf.Cos(roll * Mathf.PI * 2 / 360);
   float height = distance * Mathf.Sin(roll * Mathf.PI * 2 / 360);
   
   cameraPos.x = targetPos.x + d * Mathf.Cos(rot * Mathf.PI * 2 / 360);
   cameraPos.y = targetPos.y + height;
   cameraPos.z = targetPos.z + d * Mathf.Sin(rot * Mathf.PI * 2 / 360);
   
   Camera.main.transform.position = cameraPos;
   Camera.main.transform.LookAt(target.transform);
   ```

6. Input.GetAxis("Mouse ScrollWheel")可以获取鼠标滚轮的增量，向上滚减少，向下滚增加

7. 服务端使用Socket创建套接字时，如果是TCP方式，则为Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp)，如果是UDP方式，则为Socket(AddressFamily.InterNetwork, SocketType.Dgram, ProtocolType.Udp)；
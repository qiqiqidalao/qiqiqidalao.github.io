1. 标准着色器(Standard)主要是针对硬质表面设计，可以处理现实世界中的大多数材质，比如石头、陶瓷、铜器、银器或橡胶，皮肤、头发等。其中Standard的Albedo属性是物体表面的基本颜色，在物理模型中相当于表面的散射颜色。可以点击该属性名前方的圆圈选择贴图，也可以通过后方的方框选择颜色。Metallic属性是物体表面对光线反射的能量，通常金属物体超过50%，大部分在90%，而非金属物体则击中在20%以下。Smoonthness属性值越大，物体越光滑，反之越粗糙。normal map属性是物体的法线贴图。Emission属性表示物体是否自发光。
2. AudioSource组件中的Bypass Effects属性表示是否打开音频特效，Pitch属性表示播放速度(取值范围在-3到3之间。设置1为正常播放，小于1为减慢播放，大于1为加速播放)。
3. GUI.Button绘制按钮，常与if语句配合使用，有两个参数，第一个参数为按钮的位置和大小，第二个参数为按钮的文本。GUI.Label绘制文本，GUI.DrawTexture绘制贴图，GUI.Box绘制一个图形框，GUI.Window绘制一个窗口，GUI.TextField绘制输入框，GUI.PasswordField绘制密码输入框，GUI.HorizontalScrollBar绘制水平滚动条。
4. 
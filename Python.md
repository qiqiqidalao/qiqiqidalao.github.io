# 随笔

1. ```python
   %matplotlib inline
   import matplotlib.pyplot as plt
   #下面先生成一个从-20到20的，元素数为10的等差数列
   x = np.linspace(-20,20,10)
   #再令 y = x^3 + 2x^2 + 6x + 5
   y = x**3 + 2*x**2 + 6*x + 5
   #画出这条函数的曲线
   plt.plot(x,y, marker = "o")
   ```

   在代码开头的一行允许Jupyter Notebook进行内置实时绘图。如果不写这一行，则需在最后加入plt.show()这一句，才能让图形显示出来.

2. 
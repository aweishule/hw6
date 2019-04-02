#<center> 数字图像处理第六次作业</center>

------

<center>自动化少61</center>

<center>魏俊哲</center>

<center>2140506024</center>

<center>2019.4.2</center>

### 摘要：
本次作业学习了退化与还原图像的基本操作，使用以前学过的滤波器对高斯噪声和椒盐噪声进行处理，进一步加深对滤波器的理解。

> 1.在测试图像上产生高斯噪声lena图-需能指定均值和方差；并用多种滤波器恢复图像，分析各自优缺点；

### 原理说明
图像退化模型： 图像退化过程被建模为一个退化函数和一个加性噪声项，对一幅输入图像 f(x,y) 进行处理，产生一副退化后的图像 g(x,y)。给定 g(x,y) 和关于退化函数 H 的一些信息以及关于加性噪声项η(x,y)的一些信息，图像复原的目的就是获得原始图像的一个估计。
高斯噪声： 所谓高斯噪声是指它的概率密度函数服从高斯分布 （即正态分布） 的一类噪声。 一个高斯随 机变量 z 的 PDF 可表示为：
$P(z)={{1} \over \sqrt{2\pi\sigma}}e^{[-(z-u)^2]\over2\sigma^2}$
其中 z 代表灰度， u 是 z 的均值，是 z 的标准差。高斯噪声的灰度值多集中在均值附近。
首先利用matlab提供的 imnoise函数给图像添加高斯噪声，之后分别利用算术平均值滤波器和中值滤波器
进行滤波并观察效果。 


### 处理结果
5，0.01
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/gauss%20noise.bmp)
0，0.01
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/gauss%20noise%200.bmp)

### 结果分析
 ①首先通过 imnoise 函数分别产生了被不同均值和方差的高斯噪声污染的图像。当高斯噪声 均值不变为 0 时，随着方差增加，图像噪声越严重；当高斯噪声方差不变时，均值会影响到整个图像的灰度值，使整个图像变亮。与理论上均值和方差对图像的影响一致。 
 ②分别使用算术均值滤波器和中值滤波器对加噪图像进行恢复。 两种方法在一定程度上都可以降低噪声。算术均值滤波器降低噪声的同时也模糊了图像。 
> 2.在测试图像lena图加入椒盐噪声（椒和盐噪声密度均是0.1）；用学过的滤波器恢复图像；在使用反谐波分析Q大于0和小于0的作用；

### 原理说明
椒盐噪声也称为脉冲噪声，是图像中经常见到的一种噪声，它是一种随机出现的白点或者黑点，可能是亮的区域有黑色像素或是在暗的区域有白色像素（或是两者皆有）。盐和胡椒噪声的成因可能是影像讯号受到突如其来的强烈干扰而产生、类比数位转换器或位元传输错误等。例如失效的感应器导致像素值为最小值，饱和的感应器导致像素值为最大值。。
### 处理结果

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/saltpepper.bmp)

### 结果分析
结果发现两种滤波方法对椒盐噪声处理效果较好。中值滤波保留原图程度较好，但残留有少量椒盐噪声，算术均值滤波器降低噪声的同时也模糊了图像。

> 3.3.推导维纳滤波器并实现下边要求；
(a) 实现模糊滤波器如方程Eq. (5.6-11).
(b) 模糊lena图像：45度方向，T=1；
(c) 再模糊的lena图像中增加高斯噪声，均值= 0 ，方差=10 pixels 以产生模糊图像；
(d)分别利用方程 Eq. (5.8-6)和(5.9-4)，恢复图像；并分析算法的优缺点.

### 原理说明
维纳滤波器推导如下：
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/IMG_20190402_231010.jpg)
模糊滤波器的频域表达式为：
$H(u,v)={{T} \over {\pi(ua+vb)}}sin\pi(ua+vb)e^{-j\pi(ua+vb)}$
使用matlab提供的imfilter和fspecial实现最小二乘法。
### 处理结果
模糊lena图像：45度方向，T=1；
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/lenamohu.bmp)
再模糊的lena图像中增加高斯噪声，均值= 0 ，方差=10 pixels 以产生模糊图像；
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/lenamohugauss.bmp)
维纳滤波器：
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/信噪比.bmp)
最小二乘：
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw6/master/ercheng.bmp)

### 结果分析
维纳滤波的参数选取比较困难，可以设定步长进行搜索信噪比最大的k，但由于耗时过长，只能选取较长的步长进行尝试，粗挑发现k=0.11时信噪比最大。
图像得到了一定的改善，运动模糊的影响基本被消除，但噪声的影响仍然较大， 导致图像质量下降； 最小二乘效果稍好于维纳滤波，但图像模糊程度过大。


### 附录
参考文献：Rafael C. Gonzalez., et al. 数字图像处理（第三版）, 电子工业出版社，2011.


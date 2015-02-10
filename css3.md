##变形——旋转 rotate()
>通过指定的角度参数使元素相对原点进行旋转，正值顺时针，负值逆时针

```
-webkit-transform: rotate(45deg);
        transform: rotate(45deg);

```
##变形--扭曲 skew()
>让元素倾斜显示。它可以将一个对象以其中心位置围绕着X轴和Y轴按照一定的角度倾斜这与rotate()函数的旋转不同，rotate()函数只是旋转，而不会改变元素的形状。skew()函数不会旋转，而只会改变元素的形状。

###skew() 具有三种情况：

1. skew(x,y)使元素在水平和垂直方向同时扭曲
2. skewX(x)仅使元素在水平方向扭曲变形
3. skewY(y)仅使元素在垂直方向扭曲变形

```
-webkit-transform: skew(45deg);
   -moz-transform: skew(45deg) 
        transform: skew(45deg);
```
##变形--缩放 scale()
>让元素根据中心原点对对象进行缩放

###scale 具有三种情况

1. scale(X,Y)使元素水平方向和垂直方向同时缩放
2. scaleX(x)元素仅水平方向缩放
3. scaleY(y)元素仅垂直方向缩放

```
-webkit-transform: scale(1.5);
   -moz-transform:scale(1.5)
        transform: scale(1.5);
```

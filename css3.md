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

##变形--位移 translate()
>translate()函数可以将元素向指定的方向移动，类似于position中的relative,或以简单的理解为，使用translate()函数，可以把元素从原来的位置移动，而不影响在X、Y轴上的任何Web组件。

###translate我们三种情况

1. translate(x,y)水平方向和垂直方向同时移动
2. translateX(x)仅水平方向移动
3. translateY(Y)仅垂直方向移动

```
-webkit-transform: translate(50px,100px);
   -moz-transform: translate(50px,100px);
        transform: translate(50px,100px);
```

##变形--矩阵 matrix()
>matrix() 是一个含六个值的(a,b,c,d,e,f)变换矩阵，用来指定一个2D变换，相当于直接应用一个[a b c d e f]变换矩阵。就是基于水平方向（X轴）和垂直方向（Y轴）重新定位元素,此属性值使用涉及到数学中的矩阵.

```
-webkit-transform: matrix(1,0,0,1,50,50);
   -moz-transform: matrix(1,0,0,1,50,50);
        transform: matrix(1,0,0,1,50,50);
```
##变形--原点 transform-origin
>任何一个元素都有一个中心点，默认情况之下，其中心点是居于元素X轴和Y轴的50%处.在没有重置transform-origin改变元素原点位置的情况下，CSS变形进行的旋转、位移、缩放，扭曲等操作都是以元素自己中心位置进行变形。但很多时候，我们可以通过transform-origin来对元素进行原点位置改变，使元素原点不在元素的中心位置，以达到需要的原点位置。

```
-webkit-transform-origin: left top;
        transform-origin: left top;
```
##动画--过渡属性 transition-property
>CSS3的过度transition属性是一个复合属性，主要包括以下几个子属性：

1. transition-property:指定过渡或动态模拟的CSS属性
2. transition-duration:指定完成过渡所需的时间
3. transition-timing-function:指定过渡函数
4. transition-delay:指定开始出现的延迟时间

>transition-property用来指定过渡动画的CSS属性名称，而这个过渡属性只有具备一个中点值的属性（需要产生动画的属性）才能具备过渡效果，其对应具有过渡的CSS属性主要有:

| 属性名称            | 类型            |
| ------------------- | --------------- |
| background-color    | color           |
| background-image    | only gradients  |
| background-position | percentage, length |
| border-bottom-color | color |
| border-bottom-width | length |
| border-color | color |
| border-left-color | color |
| border-left-width | length |
| border-right-color | color |
| border-right-width | length |
| border-spacing | length |
| border-top-color | color |
| border-top-width | length |
| border-width | length |
| bottom | length, percentage |
| color | color |
| crop | rectangle |
| font-size | length, percentage |
| font-weight | number |
| grid-* | various |
| height | length, percentage |
| left | length, percentage |
| letter-spacing | length |
| line-height | number, length, percentage |
| margin-bottom | length |
| margin-left | length |
| margin-right | length |
| margin-top | length |
| max-height | length, percentage |
| max-width | length, percentage |
| min-height | length, percentage |
| min-width | length, percentage |
| opacity | number |
| outline-color | color |
| outline-offset | integer |
| outline-width | length |
| padding-bottom | length |
| padding-left | length |
| padding-right | length |
| padding-top | length |
| right | length, percentage |
| text-indent | length, percentage |
| text-shadow | shadow |
| top | length, percentage |
| vertical-align | keywords, length, percentage |
| visibility | visibility |
| width | length, percentage |
| word-spacing | length, percentage |
| z-index | integer |
| zoom | number |

```
div {
  width: 200px;
  height: 200px;
  background: red;
  margin: 20px auto;
  -webkit-transition-property: height;
          transition-property: height;
  -webkit-transition-duration: .5s;
          transition-duration: .5s;
  -webkit-transition-timing-function: ease-in;
          transition-timing-function: ease-in;
  -webkit-transition-delay: .18s;
  	  transition-delay: .18s;
}
div:hover {
  height: 400px;
}
```

##动画--过渡所需时间 transition-duration
>用来设置一个属性过渡到另一个属性所需的时间，也就是从旧属性过渡到新属性花费的时间长度，俗称持续时间。

```
-webkit-transition-duration: 1s;
        transition-duration: 1s;
```

##动画--过渡函数 transition-timing-function
>transition-timing-function属性指的是过渡的“缓动函数”。主要用来指定浏览器的过渡速度，以及过渡期间的操作进展情况，其中要包括以下几种函数:

| 函数名称            | 备注            |
| ------------------- | --------------- |
|linear|线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)|
|ease：|平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0)|
|ease-in：|由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)|
|ease-out：|由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0)|
|ease-in-out：|由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)|
|cubic-bezier(number, number, number, number)：|特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内|

```
div {
  width: 200px;
  height: 200px;
  background-color: orange;
  margin: 20px auto;
  border-radius: 100%;
  -webkit-transition-property: -webkit-border-radius;
          transition-property: border-radius;
  -webkit-transition-duration: 1s;
          transition-duration: 1s;
  -webkit-transition-timing-function: ease-in;
          transition-timing-function: ease-in;
  -webkit-transition-delay: .2s;
          transition-delay: .2s;
}
div:hover {
  border-radius: 0px;
}
```

##动画--过渡延迟时间 transition-delay
>transition-delay属性和transition-duration属性极其类似，不同的是transition-duration是用来设置过渡动画的持续时间，而transition-delay主要用来指定一个动画开始执行的时间，也就是说当改变元素属性值后多长时间开始执行。
有时我们想改变两个或者多个css属性的transition效果时，只要把几个transition的声明串在一起，用逗号（“，”）隔开，然后各自可以有各自不同的延续时间和其时间的速率变换方式。但需要值得注意的一点：第一个时间的值为 transition-duration，第二个为transition-delay。

```
a{ transition: background 0.8s ease-in 0.3,color 0.6s ease-out 0.3;}
```
```
.wrapper {
  width: 400px;
  height: 400px;
  margin: 20px auto;
  border: 2px dotted red;
}
.wrapper div {
  width: 200px;
  height: 200px;
  background-color: orange;
  -webkit-transition: all .28s ease-in .1s;
  transition: all .28s ease-in .1s;
}
.wrapper div:hover {
  width: 300px;
  height: 300px;
  background-color: red;
}
```

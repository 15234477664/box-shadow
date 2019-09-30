# box-shadow（box-shadow制作各种单边，多边阴影）
## box-shadow问题探究
box-shadow 在MDN定义以及详解：

box-shadow 以由逗号分隔的列表来描述一个或多个阴影效果。该属性让你可以对几乎所有元素的边框产生阴影。如果元素同时设置了

border-radius ，阴影也会有圆角效果。多个阴影的z-ordering 和多个 text shadows 规则相同(第一个阴影在最上面)。inset默认阴影在边框外。

参数：

<offset-x> 设置水平偏移量，如果是负值则阴影位于元素左边。 
  
<offset-y> 设置垂直偏移量，如果是负值则阴影位于元素上面。可用单位请查看 <length> 。如果两者都是0，那么阴影位于元素后面。这时如果设置了<blur-radius> 或<spread-radius> 则有模糊效果。
  
<blur-radius>模糊半径值越大，模糊面积越大，阴影就越大越淡。 不能为负值。默认为0，此时阴影边缘锐利。
  
<spread-radius>扩展半径取正值时，阴影扩大；取负值时，阴影收缩。默认为0，此时阴影与元素同样大。
  
<color>相关事项查看 <color> 。如果没有指定，则由浏览器决定——通常是color的值，不过目前Safari取透明。
  
使用 inset 后，阴影在边框内（即使是透明边框），背景之上内容之下。

阴影大小

<spread-radius>才是用来控制阴影大小（扩展还是缩小）。如果没有设置扩展半径，那么阴影尺寸与元素大小相同。
```css
.shadow{
width:40px;
height:40px;
margin:100px auto;
border:2px solid orange;
box-shadow:50px 50px 0px 0px #00ff00;
}
```
效果如下：
  
![Image text](https://github.com/15234477664/box-shadow/blob/master/img/1.png)
模糊半径是否影响阴影大小？

只要没有设置扩展半径，阴影实际的大小不改变。<blur-radius>的值用来控制模糊程度，并不控制阴影的大小。<blur-radius>就类似于于photoshop中的羽化半径。
```css
.shadow1{
width:40px;
height:40px;
margin:100px auto;
border:2px solid orange;
box-shadow:50px 50px 10px 0px #00ff00, -50px 50px 40px 0px #00ff00;
}
```
扩展半径正负值对阴影大小的影响
```css
.shadow1{
    width:40px;
    height:40px;
    margin:100px auto;
    border:2px solid orange;
    box-shadow:60px 60px 0 10px #00ff00;
}
.shadow2{
    width:40px;
    height:40px;
    margin:100px auto;
    border:2px solid orange;
    box-shadow:60px 60px 0 -10px #00ff00;
}
```
扩展半径如果是正的值，阴影扩展，如原来总宽高为44px的元素（包括边框2px），在设置10px扩展半径后，阴影的宽高会变为64px。
  
扩展半径如果是负的值，阴影收缩，如原来总宽高为44px的元素（包括边框2px），在设置-10px半径后，阴影的宽高会变为24px。
## 阴影问题解决
制作单边阴影时候常遇见这样一个情况，明明设置了x,y轴方向的偏移，为什么别的边还是有阴影出现。
```css
.shadow1{
    width:100px;
    height:100px;
    margin:100px auto;
    border:2px solid orange;
    box-shadow:3px 10px 10px 0 #00ff00;
}
```
如果不想边框左边出现任何绿色阴影，那么我们需要将x方向的偏移量调大一下。
```css
.shadow1{
    width:100px;
    height:100px;
    margin:100px auto;
    border:2px solid orange;
    box-shadow:8px 10px 10px 0 #00ff00;
}
```
可是元素右边的阴影太多了，如果将x偏移量改小了，左边就会出现阴影。

这种进退维谷的情况让人很奔溃。这其实模糊半径带来的问题，在设置模糊半径的时候（没有设置偏移量和扩展半径），发现元素四周会有阴影（羽化）的效果。

为了解决这个问题我们会不停调整左右的偏移量，其实我们应该调整元素扩展半径，让它变为负值，缩小阴影尺寸。
```css
.shadow1{
    width:100px;
    height:100px;
    margin:100px auto;
    border:2px solid orange;
    box-shadow:3px 10px 10px -2px #00ff00;
}
```
## 制作阴影
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
    </head>
    <style>
        .shadow div{
            float:left;
            margin:50px 120px;
            width:100px;
            height:100px;
            border:2px solid orange;
            text-align:center;
            line-height:100px;
         }
        .left{
            box-shadow:-5px 0 10px -5px #00ff00;
        }
        .bottom{
            box-shadow:0 5px 10px -5px #00ff00;
        }
        .right{
            box-shadow:5px 0 10px -5px #00ff00;
        }
        .top{
            box-shadow:0px -5px 10px -5px #00ff00;
        }
        .left-top{
            box-shadow:-5px -5px 10px  -4px #00ff00;            
        }        
        .right-top{
            box-shadow:5px -5px 10px -4px #00ff00;
        }
        .left-bottom{
            box-shadow:-5px 5px 10px -4px #00ff00;
        }
        .right-bottom{
            box-shadow:5px 5px 10px -4px #00ff00;
        }
        .no-left{
            /* .right-bottom,.right-top组合 */
            box-shadow:5px 5px 10px -4px #00ff00,5px -5px 10px -4px  #00ff00;
        }
        .no-bottom{
            /* .left-top,.right-top组合 */
            box-shadow:-5px -5px 10px  -4px #00ff00,5px -5px 10px -4px  #00ff00;
        }
        .no-right{
            /* .left-top，.left-bottom组合 */
            box-shadow:-5px -5px 10px  -4px #00ff00,-5px 5px 10px -4px #00ff00;
        }
        .no-top{
            /* .left-bottom,,right-bottom组合 */
            box-shadow:-5px 5px 10px -4px #00ff00,5px 5px 10px -4px #00ff00;
        }
    </style>
    <body>
    <div class="shadow">
        <div class="left">左边阴影</div>
        <div class="bottom">底部阴影</div>
        <div class="right">右部阴影</div>
        <div class="top">顶部部阴影</div>
        <div class="left-top">左上阴影</div>
        <div class="right-top">右上阴影</div>
        <div class="left-bottom">左下阴影</div>
        <div class="right-bottom">右下阴影</div>
        <div class="no-left">无左阴影</div>
        <div class="no-bottom">无下阴影</div>
        <div class="no-right">无右阴影</div>
        <div class="no-top">无上阴影</div>        
    </div>
    </body>
</html>
```

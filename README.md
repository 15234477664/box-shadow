# box-shadow（box-shadow问题探究（box-shadow制作各种单边，多边阴影））
```html
box-shadow 在MDN定义以及详解：
box-shadow 以由逗号分隔的列表来描述一个或多个阴影效果。该属性让你可以对几乎所有元素的边框产生阴影。如果元素同时设置了 border-radius ，阴影也会有圆角效果。多个阴影的z-ordering 和多个 text shadows 规则相同(第一个阴影在最上面)。inset默认阴影在边框外。
参数：
<offset-x> 设置水平偏移量，如果是负值则阴影位于元素左边。 
<offset-y> 设置垂直偏移量，如果是负值则阴影位于元素上面。可用单位请查看 <length> 。如果两者都是0，那么阴影位于元素后面。这时如果设置了<blur-radius> 或<spread-radius> 则有模糊效果。
<blur-radius>模糊半径值越大，模糊面积越大，阴影就越大越淡。 不能为负值。默认为0，此时阴影边缘锐利。
<spread-radius>扩展半径取正值时，阴影扩大；取负值时，阴影收缩。默认为0，此时阴影与元素同样大。
<color>相关事项查看 <color> 。如果没有指定，则由浏览器决定——通常是color的值，不过目前Safari取透明。
使用 inset 后，阴影在边框内（即使是透明边框），背景之上内容之下。
```


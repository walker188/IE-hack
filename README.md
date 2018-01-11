# IE-hack
ie浏览器兼容笔记
haslayout 问题的调试与解决
当网页在 IE 中有异常表现时，可以尝试激发 haslayout 来看看是不是问题所在。常用的方法是给某元素 css 设定 zoom:1 。
使用 zoom:1 是因为大多数情况下，它能在不影响现有环境的条件下激发元素的 haslayout。而一旦问题消失，那基本上就可以判断是 haslayout 的原因。
然后就可以通过设定相应的 css 属性来对这个问题进行修正了。建议首先要考虑的是设定元素的 width/height 属性，其次再考虑其他属性。

对 IE6 及更早版本来说，常用的方法被称为霍莉破解(Holly hack)，即设定这个元素的高度为 1% (height:1%;)。需要注意的是，
当这个元素的 overflow 属性被设置为 visible 时，这个方法就失效了。或者使用 IE 的条件注释。
对 IE7 来说，最好的方法时设置元素的最小高度为 0 (min-height:0;)。

haslayout 问题引起的常见 bug

IE6 及更低版本的双空白边浮动 bug
bug 修复: display:inline;

IE5-6/win 的 3 像素偏移 bug
bug 修复: _height:1%;

E6 的躲躲猫(peek-a-boo) bug
bug 修复: _height:1%;

1、解决ie7不支持display:inline-block;
第一种：
 display:inline-block;
 *display:inline;
 *zoom:1;
特别是 ZOOM:1 这个必须的（总是触发layout），具有“layout” 的元素如果同时 display: inline ，那么它的行为就和标准中所说的 inline-block 很类似了。
第二种：
.selector { display: inline-block }
.selector { *display: inline }
注意这两个 display要先后放在两个CSS声明中才有效果，这是IE的一个经典bug，
如果先定义了display:inline-block，然后再将 display设回inline或block，layout不会消失。不能写进一个声明中。

2、IE8下td单元格设置position:relative后导致单元格边框消失

 解决办法：td单元格去除position:relative后，将要定位的元素使用position:absolute后，不设置left、top。。。，此时使用margin进行偏移。
 
 3、

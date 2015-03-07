#Js4wap.js API

##导航
* [$()](#_1)
* [addClass](#addClass)
* [removeClass](#removeClass)
* [find](#find)
* [parent](#parent)
* [children](#children)
* [prev](#prev)
* [next](#next)
* [each](#each)
* [html](#html)
* [offset](#offset)
* [width](#width)
* [height](#height)
* [top](#top)
* [left](#left)
* [css](#css)
* [on](#on)
* [off](#off)
* [swipe](#swipe)


开发版：[https://github.com/Teddywow/Js4wap/blob/master/src/js4wap.js](https://github.com/Teddywow/Js4wap/blob/master/src/js4wap.js)
压缩版：[https://github.com/Teddywow/Js4wap/blob/master/src/js4wap.min.js](https://github.com/Teddywow/Js4wap/blob/master/src/js4wap.min.js)

###$()
`$(selector) => collection`

通过执行css选择器，包装dom节点，返回一个Zepto集合对象。
```
$('div') //=> 所有页面中的div元素
$('#aa') //=> ID为"aa"的元素
$('.bb') //=> 所有页面中类名含有"bb"的元素
$('#aa>div') //=> ID为"aa"的子元素内所有div元素
```

>* 如果$变量尚未定义，Js4wap会设置了全局变量$指向它本身。若$变量已经定义指向其他对象，Js4wap不会覆盖掉$，会设置全局变量Js4wap指向它本身。
>* $()函数不能用于创建元素。

###addClass

`addClass(className) => self`

为每个匹配元素添加指定的class类名，当要添加多个类名时，使用空格分隔
```
$('li').addClass('item') //=> 为页面所有li元素添加类名"item"
$('ul').addClass('box list') //=> 为页面所有ul元素添加类名"box"和"list"
```

###removeClass

`removeClass(className) => self`

为每个匹配元素移除指定的class类名，当要移除多个类名时，使用空格分隔
```
$('li').removeClass('item') //=> 为页面所有li元素移除类名"item"
$('ul').removeClass('box list') //=> 为页面所有ul元素移除类名"box"和"list"
```

###find
`find(selector) => collection`

查找每个匹配元素后代中符合CSS选择器的元素。
```
$('div').find('.aa') //=> 查找页面所有div元素的后代中含有类名"aa"的元素
```

###parent
`parent() => collection`

返回对象集合中每个元素的直接父元素。

###children
`children() => collection`

返回每个匹配元素集合元素的直接子元素。

###prev
`prev() => collection`

返回对象集合中每一个元素的前一个兄弟节点。

###next
`next() => collection`

返回对象集合中每一个元素的后一个兄弟节点。

###each
`each(function(index, item){ ... }) => self`

遍历一个对象集合每个元素。在迭代函数中，函数第一个参数index指向当前项在对象集合的位置，函数的第二个参数item和this关键字指向当前项。
```
$(".aa").each(function(index,item){
	console.log(index,item,this);
})
```

###html
`html() => array`
`html(content) => self`

获取或设置对象集合中元素的HTML内容。当没有给定content参数时，返回一个包含对象集合中每个元素内容的数组。当给定content参数时，用其替换对象集合中每个元素的内容。

###offset
`offset() => object`

返回对象集合中第一个元素相对于document的位置。返回一个对象含有： width, height, top和left。
```
$('#item').offset //=> {width: 1080, height: 18, top: 144, left: 8}
```

###width
`width() => number`

返回对象集合中第一个元素的宽度。
```
$('#item').width() //=> 1080
//相当于
$('#item').offset().width //=> 1080
```

###height
`height() => number`

返回对象集合中第一个元素的高度。
```
$('#item').height() //=> 18
//相当于
$('div>.item').offset().height //=> 18
```

###top
`top() => number`

返回对象集合中第一个元素的上边界和document的上边界间的距离。
```
$('#item').top() //=> 144
//相当于
$('#item').offset().top //=> 144
```

###left
`left() => number`

返回对象集合中第一个元素的左边界和document的左边界的距离。
```
$('#item').left() //=> 8
//相当于
$('#item').offset().left //=> 8
```

###css
`css(property) => value`
`css(property , value) => self`

读取或设置DOM元素的css属性。当value参数不存在的时候，返回对象集合中第一个元素的css属性。当value参数存在时，设置对象集合中每一个元素的对应css属性。

当value为空(空字符串，null 或 undefined)，那个css属性将会被移出。
```
var w;
$('#item').css('width') //=> 1080
$('.item').css('width','100') //=> 为类名为item的每个元素设置`width`为100px。
$('.item').css('width','') //=> 为类名为item的每个元素移除`width`属性。
$('.item').css('width',w) //=> 为类名为item的每个元素移除`width`属性。
```

###on
`on(event,fn,type) => self`

为对象集合中得元素绑定事件。

* event：定义绑定到匹配元素中的事件类型。
* fn：定义当事件发生时运行的方法。
* type：定义在捕捉过程还是冒泡过程执行事件，true为在捕捉过程，false为在冒泡过程，默认为false。 

```
function cFn(){...}
$('.item').on('click',cFn,false);

$('.item').on('click',function(e){
	alert('hi');	
},false);
```

###off
`off(event,fn,type) => self`

为对象集合中的元素移除通过 on 添加的事件，必须通过用on()添加的那个相同的函数。
三个参数必须要跟on()的参数相同，否则会出错。要求要移除的事件在用on()绑定时function不能是匿名函数。
```
function cFn(){...}
$('.item').on('click',cFn,false);
$('.item').off('click',cFn,false);
```

###swipe
`swipeLeft(fn,data) => self`
`swipeRight(fn,data) => self`
`swipeUp(fn,data) => self`
`swipeDown(fn,data) => self`

当对象集合中得元素被划过时触发（可选择给定方向）
```
$('.item').swipeDown(function(data){
	console.log('down,'+data);
},"mes")
```


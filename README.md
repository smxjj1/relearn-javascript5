1.Document	Object	 Model ：了解DOM树是什么意思
文档对象模型：DOM是一套可以操作文档的工具箱
Document：文档，就是html文件
2.分清楚元素和节点代表什么意思?
节点：文档中所有的内容都是节点。（标签（元素）节点，文本节点，注释节点，属性节点）

元素：文档中的标签叫做元素
学习目标:
1.使用document.getElementById获取有id的元素
getElementById：通过id获取元素
2.通过console.dir查看元素对象的默认属性
Console.dir是以对象形式展示元素

Console.log:通过标签形式，可以很方便的定位到页面上的位置
Console.dir通过对象形式，可以很方便的看到具体属性
3.理解小猫发威案例的需求；
Img标签原本的src属性是小猫，然后通过在js中设置img.src属性为老虎。

从此可以知道，标签的属性可以获取也可以设置：
console.log(demo.src); // 获取属性
demo.src = "images/tiger.png"; //设置属性


学习目标:
1.使用正确的格式书写代码
建议将script代码放到body底部，以免出现问题。
2.网页加载顺序对网页的执行有所影响
<img src="images/kitty.png" id="demo" alt=""/>
<script>
    var demo = document.getElementById("demo");
    demo.src = "images/tiger.png";
</script>

以上代码如果将script放到img上边，会出现以下问题：

原因为何？
这是因为，解析器解析html从上至下，解析带demo的时候，发现还没有id为demo的元素，所以demo为null，null.src是错误的。
案例完善：通过鼠标点击图片更改图片的路径（为了看到小猫发威的过程）
新知识点：onclick	 鼠标单击事件（左键）
案例思路：第一步：封装一个函数（功能：图片标签改变src）；
		   第二步：函数内部，先获取盒子，再改变盒子的路径属性；
		   第三步：在图片的鼠标点击事件中调用函数；
	代码：
<img src="images/kitty.png" onclick="changePic();" id="demo" alt=""/>
<script>
    function changePic() {
        //alert("标签被点击了");
        //获取img标签 然后 控制他的src属性
        var demo = document.getElementById("demo");
        demo.src = "images/tiger.png";

    }
</script>
代码理解：当鼠标点击img之后，会触发onclick事件，然后调用changePic方法。

注意：事件执行的过程和顺序
案例：通过列表展示不同图片（基本功能），点击第二张图片更换对应大图
案例思路：第一步：封装一个函数（功能）；
		   第二步：函数内部，先获取盒子，再改变盒子的路径属性；
		   第三步：第二张图片标签添加鼠标点击事件，然后调用函数；
	代码：
//点击下面的小图片 让上面的大图片显示相应的大图
//1.给img设置onclick属性 点击第二个图片 让上面的img的src变为对应的大图
function changePic() {
    //alert("a");
    //找人
    var bigImg = document.getElementById("bigImg");
    //控制src属性
    bigImg.src = "images/02big.jpg";
}
	效果：
	
案例升级：通过盒子多次调用，传递不同参数，更改不同的图片
案例思路：第一步：函数添加参数imgName，代表不同图片
第二步：让列表的所有图片都添加点击事件，调用封装的函数；
		   第三步：传递实参，在函数内部接收实参，然后拼接字符串；
	代码：
//点击下面的小图片 让上面的大图片显示相应的大图
//1.给img设置onclick属性 点击第二个图片 让上面的img的src变为对应的大图
function changePic(imgName) {
    //alert("a");
    //找人
    var bigImg = document.getElementById("bigImg");
    //控制src属性
    bigImg.src = "images/0"+imgName+"big.jpg";
}

<ul id="itemList">
    <li><img src="images/01.jpg" onclick="changePic(1);" alt=""/></li>
    <li><img src="images/02.jpg" onclick="changePic(2);" alt=""/></li>
    <li><img src="images/03.jpg" onclick="changePic(3);" alt=""/></li>
    <li><img src="images/04.jpg" onclick="changePic(4);" alt=""/></li>
    <li><img src="images/05.jpg" onclick="changePic(5);" alt=""/></li>
</ul>

学习目标：a标签跳转的目的在于禁用js后还可以实现跳转
案例思路：第一步：在a标签内部的点击事件中直接return false，检测a跳转是否被禁用
		   第二步：在a标签点击事件调用的函数内部return false，然后再return 函数()；
	代码：
<a href="http://www.baidu.com" onclick="return false;">阻止默认行为</a>
<a href="http://www.baidu.com" onclick="return test(16);">未满十八岁禁止入内</a>
<script>
    function test(age) {
        if (age > 18) {
            alert("欢迎");
        } else {
            alert("禁止");
            return false;
        }
    }
	
效果：
问题：为什么test方法以及return false了，而a标签的点击事件在处理时还需要return 方法()？
大家还记得，调用了方法，相当于调用了他的返回值么？所以这里的return test(16),就相当于return false.
案例：通过列表展示不同图片（基本功能）
js未禁用时，点击小图下方出现对应大图；js禁用时，点击小图跳转看大图。
案例思路：第一步：封装一个函数（功能）；
		   第二步：函数内部，先获取盒子，再改变盒子的路径属性；
第四步：让列表的所有图片都添加点击事件，调用封装的函数；
		   第五步：传递实参，在函数内部接收实参，然后拼接字符串；
	代码：
 <div id="box">
    <img src="images/01big.jpg" id="bigImg" alt=""/>
    <ul id="itemList">
        <li><img src="images/01.jpg" onclick="changePic(1);" alt=""/></li>
        <li><img src="images/02.jpg" onclick="changePic(2);" alt=""/></li>
        <li><img src="images/03.jpg" onclick="changePic(3);" alt=""/></li>
        <li><img src="images/04.jpg" onclick="changePic(4);" alt=""/></li>
        <li><img src="images/05.jpg" onclick="changePic(5);" alt=""/></li>
    </ul>
</div>
<script>
    //点击下面的小图片 让上面的大图片显示相应的大图
    //1.给img设置onclick属性 点击第二个图片 让上面的img的src变为对应的大图
    function changePic(imgName) {
        //alert("a");
        //找人
        var bigImg = document.getElementById("bigImg");
        //控制src属性
        bigImg.src = "images/0" + imgName + "big.jpg";
    }
</script>

	效果：
	
注意：注意此案例和京东案例的区别
	相册案例，在禁用js时，还可以跳转查看大图，这是因为img外层包裹了a标签。
学习目标:
1.掌握新知识 ： 事件源.事件 = function（） {事件处理程序}
2.事件三要素跟之前事件的区别（代码增多，但是结构和思路清晰了）
代码：
var btn = document.getElementById("btn");
//<标签 事件="事件处理程序" >
//事件源.事件 = function(){ 事件处理程序 };
btn.onclick = function () {
    //alert('1');
    console.log(this);
};

注意：要做事先找人，此结构会经常使用，一定要记下来；
问题：
为什么要使用事件三要素这种方式给元素绑定事件？

这是之前的事件绑定方式，我们发现js代码和html代码混淆在一起了。这样不方便以后的维护。所以，js和html代码需要分离。
学习目标:
1.掌握新知识 – document.getElementsByTagName
根据标签名批量获取这一类的元素。
2.区分getElementsByTagName与getElementById的用法
代码：
var btn = document.getElementById("btn");
console.log(btn);
//getElementsByTagName get Elements By Tag Name 通过标签名获取元素集合
var inputs = document.getElementsByTagName("input");//伪数组
console.log(inputs);
var arr = [1, 2, 3];
console.log(arr);
console.log(inputs instanceof Array);//不是数组
//getElements 获取到的都是 伪数组
//getElement 获取到的都是 元素对象


注意：伪数组不是数组，这里获取到的是伪数组，是HTML标签的集合，不能直接使用；
			伪数组也有length属性，也可以通过索引获取对应元素，所以可以遍历。
上图中的#btn是指当前input的id为btn。
案例：批量获取元素，批量注册事件
案例思路：第一步：通过document.getElementsByTagName拿到标签集合；
		   第二步：使用for循环遍历标签集合，将每一项拿出来给事件属性赋值一个函数；
	代码：
var inputs = document.getElementsByTagName("input");
/*inputs.onclick = function () {
 alert("a");
 };*/
//console.log(inputs);
for (var i = 0; i < inputs.length; i++) {

    inputs[i].onclick = function () {
        alert("a");
    };
}

注意：未经遍历的元素集合，不能设置任何事件；就是不能直接给inputs设置事件。
学习目标:
1.document.getElementById，只有这一种写法，不能划定范围
只能在整个文档document中根据id查找对应元素。不能划定发威，因为id是唯一的。
2.document.getElementsByTagName，可以从别的元素范围内寻找
代码：
//getElementsByTagName 可以被 document 调用 表示获取页面上 所有这一类型的标签
//var inputs = document.getElementsByTagName("input");
//console.log(inputs);
//getElementsByTagName 还可以被 普通的元素对象调用 表示获取这个元素对象内部的这一类型的标签
//var demo2 = document.getElementById("demo2");
//var inputs = demo2.getElementsByTagName("input");
//console.log(inputs);
//getElementById 不能被普通的元素对象调用 只能被document调用
var demo2 = document.getElementById("demo2");
var btn = demo2.getElementsByTagName("btn");
console.log(btn);

案例升级：通过事件三要素将案例改写；js与html分离。
案例思路：第一步：通过划定范围找到需要注册点击事件的图片；
		   第二步：通过for循环，给每一个元素注册事件；
		   第三步：函数内部，还是调用之前的函数；
		   第四步：i不能用，可以使用this.alt属性；
	代码：
	//点击下面的小图片 让上面的大图片显示相应的大图
var ul = document.getElementById("itemList");
var imgs = itemList.getElementsByTagName("img");//所有的小图片
for (var i = 0; i < imgs.length; i++) {
    //每一个小图片
    //事件源.事件 = function(){ 事件处理程序 };
    imgs[i].onclick = function () {
        //console.log(i);
        //console.log(img[i].alt);
        //console.log(this.alt);
        changePic(this.alt);
    };
}

function changePic(imgName) {
    var bigImg = document.getElementById("bigImg");
    bigImg.src = "images/0" + imgName + "big.jpg";
}

问题：为什么i不能使用？ 
changePic()方法是在什么时候调用的？for循环执行时，方法是不会被调用的。ChangePic是在图片被点击时调用的，而图片被点击时，html整个代码已经执行完毕，for循环执行完毕，这是i=imgs.length，是一个固定值。
案例完善：重写案例；之前写的有点复杂，还搞了俩方法，将两个方法合并。
案例思路：第一步：通过划定范围找到需要注册点击事件的图片；
		   第二步：通过for循环，给每一个元素注册事件；
		   第三步：函数内部，直接使用之前的代码；
	代码：
//给下面所有的小图片注册事件 点击小图片让上面的大图片的src变为和小图对应的大图
var ul = document.getElementById("itemList");
var imgs = ul.getElementsByTagName("img");//所有小图片
for (var i = 0; i < imgs.length; i++) {
    var img = imgs[i];//每一个小图
    img.onclick = function () {
        //获取大图 设置大图的src
        var bigImg = document.getElementById("bigImg");
        bigImg.src = "images/0" + this.alt + "big.jpg";
    };
}

学习目标：使用事件三要素让a标签禁止默认行为
案例思路：在a标签内部的点击事件中直接return false； 
	代码：
<a href="http://www.baidu.com" onclick="return false;">阻止默认行为</a>
<a href="http://www.baidu.com" id="demo">demo</a>
<script>
    var demo = document.getElementById("demo");
    //<标签 事件="事件处理程序">
    //事件源.事件 = function(){ 事件处理程序 };
    demo.onclick = function () {
        return false;
    };
代码理解：demo.onclick直接赋值方法，相当于就是onclick=”方法内容：return false”
案例升级：使用事件三要素让案例升级；
案例思路：第一步：通过划定范围找到需要注册点击事件的图片；
		   第二步：通过for循环，给每一个元素注册事件；
		   第三步：函数内部，直接使用之前的代码，一定要在最后return	false；
		   第四步：路径使用a标签的href，也就是this.href；
		   第五步：使用innerText改变盒子的文本；
	代码：
	//点击上面的小图片 让下面的大图片的src 变为和小图相应的大图
var ul = document.getElementById("imagegallery");
var image = document.getElementById("image");
var des = document.getElementById("des");
var links = ul.getElementsByTagName("a");
for (var i = 0; i < links.length; i++) {
    var link = links[i];
    link.onclick = function () {
        //alert("a");
        //让下面的大图片的src 变为和小图相应的大图
        image.src = this.href;
        //改变描述中的文本
        des.innerText = this.title;
        return false;//阻止跳转
    };
}
注意：innerText后期会介绍。目前只需要知道innerText可以改变标签内部文本即可。
学习目标：通过获取盒子动态设置类名，使其动态增删样式；
案例思路：第一步：先获取盒子
		   第二步：给盒子注册点击事件，给属性className赋值（样式名）；
		   第三步：使用console.dir查看盒子的相关属性；
	代码：
//点击按钮显示盒子
var btn = document.getElementById("btn");
btn.onclick = function () {
    //给盒子添加类名
    var box = document.getElementById("box");
    //console.dir(box);//class在JS中是保留字 所以类名用的是className
    box.className = "cls";
};

总结：想要设置元素的属性，可以先通过console.dir来确定属性名，再去设置或者获取。

学习目标：通过获取盒子动态设置类名，使盒子隐藏；
案例思路：第一步：先获取盒子，按钮
		   第二步：给按钮添加点击事件，给盒子className属性赋隐藏样式。
	思考：如何实现切换功能？
			切换功能，需要知道当前状态，那如何知道当前状态是隐藏还是显示呢？
案例升级：通过判断盒子内的value值，让盒子实现切换隐藏、显示功能；
案例思路：第一步：先获取盒子，按钮
		   第二步：给按钮添加点击事件，判断盒子的value值是隐藏还是显示
	   第三步：根据盒子的value设置隐藏、显示样式
代码：
//点击按钮 实现显示隐藏切换
//点击按钮 隐藏盒子
var btn = document.getElementById("btn");
var box = document.getElementById("box");
btn.onclick = function () {
    if (btn.value === "隐藏") {//如果此时按钮中的文字是隐藏 就应该隐藏盒子
        box.className = "hide";
        btn.value = "显示";
    } else {
        box.className = "show";
        btn.value = "隐藏";
    }
};

补充：盒子就是对象，js万物皆对象，盒子有很多的默认属性；
问题：此时将btn改成this可不可以？
	  当然可以。This代表当前方法所属对象。
案例：新功能 – 鼠标经过显示二维码，鼠标离开隐藏二维码
		新知识点：鼠标经过 onmouseover事件		鼠标离开	onmouseout事件
案例思路：第一步：先获取控制二维码显示隐藏的盒子
		   第二步：给盒子注册鼠标经过事件，给二维码的className添加显示样式；
	   第三步：给盒子注册鼠标离开事件，给二维码的className添加隐藏样式；
代码：
//找人
var node = document.getElementById("node_small");
var er = document.getElementById("er");
//鼠标经过父盒子 让二维码显示 onmouseover 鼠标经过事件
node.onmouseover = function () {
    er.className = "erweima show";
};
//鼠标离开父盒子 让二维码隐藏 onmouseout 鼠标离开事件
node.onmouseout = function () {
    er.className = "erweima hide";
};

问题：这里代码的缺陷是什么？er.className=”erweima show”
	这里在js中写死二维码的样式为erweima，如果后期样式名修改，还得来修改js中的代码。
学习目标：掌握操作字符串方法 replace 替换类型；
案例：优化显示隐藏二维码案例，解决缺陷。
案例思路：使用字符串方法 replace将类名更换； 
代码：
//找人
var node = document.getElementById("node_small");
var er = document.getElementById("er");
//鼠标经过父盒子 让二维码显示 onmouseover 鼠标经过事件
node.onmouseover = function () {
    //er.className = "erweima show";
    //让二维码显示 把hide替换成show
    er.className = er.className.replace("hide", "show");
};
//鼠标离开父盒子 让二维码隐藏 onmouseout 鼠标离开事件
node.onmouseout = function () {
    //er.className = "erweima hide";
    //让二维码隐藏 把show替换成hide
    er.className = er.className.replace("show", "hide");
};

总结：此两种方法结果一样，策略不同，值得注意；
注意：这里的写法还有缺陷，后期课程还会进行优化。
	   replace会替换字符串中第一个匹配的内容，那如果这里二维码原本的样式是：erweima showxxx show；showxxx是另外的一个样式，而我们要替换的是show，但是我们只要replace，他会替换的这是showxxx中的show，就会出现问题。

javascript这个磨人小妖精
---

说实话，再你熟悉了C C++ java python后再学js，总是会有无数错觉，总觉得它的语法像什么，又不太像。作为动态语言又没python那么简洁，里面很多语法借鉴了c和java的那套，但是又不像c那么严格。js是弱类型语言，而且还是有一些动态语言的灵活性在里面。

如果带着之前学C++/java的思路去学js，总觉得十分别扭，特别是它的object和function，真是让人摸不着头脑。

所以说啊，js真是个磨人的小妖精。要征服这个小妖精还真不是一时半会能实现的，所以，还是慢慢来吧，把征服它的过程都记录一下。

#语法
目前大多语言都是类C的，js也一样（除了python ruby这些自成一派的）

- 区分大小写
- 变量不区分类型，和python一样（python不用写var）
- 每条语句结尾可以省略分号
- 注释与C,C++,java,php相同
- 代码段要封闭与C,C++,java同（和python不一样）
- 运算符完全和C一致，有自加自减，有逗号表达式，有条件运算符！！（和python不一样）
- 逻辑运算符，条件，循环语句和C一致（和python不一样）
- 有switch-case语句（和python不一样）



#数组
js的数组和python的list一样可以存不同类型不同维度个数据，除了可以用下标查看修改数据外，还有几个方法：
- push()：加到最后
- pop():  从最后取
- shift(): 从开头取
- unshift(): 加入开头

#范围
在function之外的是全局变量，否则是局部变量
注意：如果没加var 默认是全局变量！

	// Declare your variable here
	var myGlobal= 10;
	
	function fun1() {
	  // Assign 5 to oopsGlobal Here
	  oopsGlobal = 5;
	}
	
	// Only change code above this line
	function fun2() {
	  var output = "";
	  if (typeof myGlobal != "undefined") {
	    output += "myGlobal: " + myGlobal;
	  }
	  if (typeof oopsGlobal != "undefined") {
	    output += " oopsGlobal: " + oopsGlobal;
	  }
	  console.log(output);
	}

#输出
console.log()

#严格相等
严格相等（===）不仅比较值，还比较类型

因为在js中，7 == “7”  

#undefined
js中有undefined，当一个变量没定义的时候，可以用下面方法判断


	if(typeof(value)=="undefined"){
	
	alert("undefined");
	
	} 

#Object 和 json
js中的object数据结构就类似其他语言中的map，hashmap，是一个键值对应的结构。javascript Object notation(JSON)其实也就是指在js中使用的这种数据交换的类型。

访问的方式一般有两种
- "." 如果是单纯的数字或者没空格的字符串，可以用
- "[]" 带空格的就要用"[]"了。

举例：

	var ourDog = {
	  "name": "Camper",
	  "legs": 4,
	  "tails": 1,
	  "friends": ["everything!"]
	};
    var name = ourDog.name;  
    name = ourDog["name"];
    var prop= "name";
    name = ourDog[prop];
    

你可以用Array或object嵌套

	var myStorage = {
	  "car": {
	    "inside": {
	      "glove box": ["maps","phone"],
	      "passenger seat": "crumbs"
	     },
	    "outside": {
	      "trunk": "jack"
	    }
	  }
	};
	
	// get maps

	var gloveBoxContents = myStorage.car.inside["glove box"][0]; 


如果要删除一个属性，用delete

	delete ourDog.tails;
	
如果增加属性，直接使用"."和"[]"就好了，和python差不多

如果要看某个属性存在不存在 hasOwnProperty()：
	
	myObj.hasOwnProperty("top");

由于object的属性和map很像，因此你可以用它来做查表操作：

	var alpha = {
	  1:"Z",
	  2:"Y",
	  3:"X",
	  4:"W",
	  ...
	  24:"C",
	  25:"B",
	  26:"A"
	};
	alpha[2]; // "Y"
	alpha[24]; // "C"

#随机数
js中的随机数是用Math.random()生成的，同样，也是返回(0,1)，如果要某个范围，可以用下面的方法

	Math.floor(Math.random() * (ourMax - ourMin + 1)) + ourMin;

#正则
js的正则是用的//，很庆辛的发现和vim很像，比如查找"in"可以用下面的正则：
	
	var testString = "How many non-space characters are there in this sentence?";	
	var expression = /in/gi;  
	var nonSpaceCount = testString.match(expression).length;

“/ /”包含的是正则内容

g 是全局

i 表示忽略大小写


正则表达式都差不多，基本和python一致
除了 \* . +
\d表示数字
\D表示非数字 
\s表示空格
\S表示非空格



#面向对象
js可以直接用之前说的方式直接声明一个Object对象
```
	var car = {
	  "wheels":4,
	  "engines":1,
	  "seats":5
	};
```

也可以用构造函数的方法：
```
	var Car = function() {
	  this.wheels = 4;
	  this.engines = 1;
	  this.seats = 1;
	};
```

创建实例直接用new就行了，然后创建的实例可以直接添加新的属性。
```
var Car = function() {
  this.wheels = 4;
  this.engines = 1;
  this.seats = 1;
};

var myCar = new Car();
myCar.nickname = "coolcar";
```


私有变量，还记得var吗？如果在类中用var就是局部变量了，也就意味着是私有变量了。
```
	var Car = function() {
	  // this is a private variable
	  var speed = 10;
	
	  // these are public methods
	  this.accelerate = function(change) {
	    speed += change;
	  };
	
	  this.decelerate = function() {
	    speed -= 5;
	  };
	
	  this.getSpeed = function() {
	    return speed;
	  };
	};
```



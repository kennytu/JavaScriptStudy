# JavaScriptStudy

基礎
====
* 一個經典的HTML包含javascript的範例
		
		<!DOCTYPE html>
		<html>
		<head lang="en">
    		<meta charset="UTF-8">
    		<title></title>
		</head>
		<body>

		<script type="text/javascript" src="js/example.js"></script>
		</body>
		</html>

> 關於<head lang="en"> 請參考 [w3c ref language codes](http://www.w3schools.com/tags/ref_language_codes.asp)

* 將javascript的引用放在body結尾之前,例如

		<body>
		<script type="text/javascript"src="mytest.js"></script>
		</body>

* 延遲腳本的寫法: 加入 defer="defer", 瀏覽器會在碰到/html之後才進行載入, 但是會在DOMConetneLoaded事件之前
 
		<script type="text/javascript" defer="defer" src="example1.js"></script> 


* HTML5定義新的元素 async, 和defer類似, 但只適用於外部腳本文件, async的腳本並不按照指定他們的先後順序執行

		<script type="text/javascript" async src="example1.js"></script> 

* 標識符, 第一個字符必須是一個字母, 下劃線(**_**), 或一個美元符號(**$**). 所以, **$abc** 是合法的變數名稱, 沒有其他含意

* typeof, usage: typeof(object) or typeof object, 有以下幾種
	1. **undefined** 
	2. **boolean** 
	3. **string**
	4. **number**
	5. **object**
	6. **function**

	example:

		var message = "some string"
		alert(typeof message);  //return "string"
		alert(typeof(message)); //return "string"
		alert(typeof 95); //return "number"

* Undefined: 使用var宣告變數但還未指定值
* 
		var message;
		alert(message == undefined); //true
		
		function foo(x, y){
			//do something
		}

		foo(); //沒有傳任何值進去,
		這時候x, y都是undefined

* 若使用一個沒有定義的變數, 會產生錯誤, 不要和undefined搞混了
* 對於沒有定義的變數, 使用任何操作都會發生錯誤, 除了使用typeof之外
	
		var message;
		//var age
		alert(typeof message); //undefined
		alert(typeof age);     //undefined

* 小技巧: 對於我們宣告的變數都要給予初始值, 這樣若我們使用typeof的時候, 出現undefined, 那我們就知道這個變數還沒有被宣告出來


* Null類型, 使用typeof測試null, 會回傳object. 另外, ECMA-262規定, null == undefined要傳回true.  

		var car = null;
		alert(typeof car); // return "object"

* 在任何時候, 若還不確定變數要付予什麼值, 設定成null是比較好的選擇


* Boolean類型, 小寫的true 以及小寫的false, 大寫的True / False會被視為變數名稱. 

* Boolean() Function, 有底下原則
	1. Boolean(true) return true
	2. Boolean(false) return false
	3. Boolean("非空字串) return true / ""(空字串) return false
	4. Boolean(Number) return true / Boolean(0 / NaN) return false
	5. Boolean(object) return true / Boolean(null) return false

	example:
		
		var message = "Hello World!";
		if (message){
			aler("Value is true);
		}
		
		//if判斷式會隱性使用Boolean()轉換, 若判別的是object, 則永遠會為true,要小心使用


	
*  Number類型
	*  8進制: var octalNum1 = 070, 0開頭, 後面要是(0 ~ 7)的組合,超過7會被解釋成10進制, 例如 var octalNum2 = 079, 會被解析成79
	*  16進制: 以0x開頭


* 浮點數: 和C語言一樣

* 數值範圍:
	* 最大: Number.MAX_VALUE
	* 最小: Number.MIN_VALUE
	* 超出最大, JavaScript表示為 Infinity
	* 超出最小, JavaScript表示為 -Infinity
	* 使用 isFinite()確認數值是否在最大以及最小中間
	
	example:

		var result = Number.MAX_VALUE + Number.MAX_VALUE;
		alert(isFinite(result)); // return false


* __NaN__ : Not a Number, 非數值, 是一個特殊的數值, 用來表是一個本來要返回數值的操作卻沒有返回數值(這樣就不會拋出錯誤), 例如, 在其他語言, 任何數值 / 0 都匯導致錯誤, 但在ECMAScript中, 任何數值 / 0會返回NaN

* 任何涉及NaN的操作都會return NaN, 另外, NaN與任何值都不相等, 包括NaN本身

		alert(NaN == NaN) //return false

* 使用isNaN, 不能被轉換為數值的都會return true. isNaN本身, 先調用valueof, 在調用toString, 都不行, 就是true
* 
		isNaN(NaN); //return true
		isNaN(10); //false
		isNaN("10"); //false 可以轉成10 
		isNaN("blue"); //true
		isNaN(true); //false  可以轉成1

* Number() & parserInt()

* Number的規則
	* 若字串只包含數字, 浮點數, 則轉成相對應的數字以及浮點數
	* 若字串包含0x, 則會做16進制對10進制的轉換
	* 空字串轉換為0
	* 不是以上轉換為NaN
 
<p>

* parserInt的規則   
	*  空字串轉換為NaN
	*  字串前面包含數字,後面有文字, 只會解析前面的數字
	*  字串包含0x視為16進制
	*  字串前導字為0, 視為8進制
<p>
*  請明確指定parserInt的進制, 例如

		var num = parseInt("0xAF", 16); //return 175
		var num1 = parseInt("10", 2);      //2  （按二进制解析） 
		var num2 = parseInt("10", 8);       //8  （按八进制解析） 
		var num3 = parseInt("10", 10);      //10 （按十进制解析） 
		var num4 = parseInt("10", 16);      //16 （按十六进制解析）

* parserFloat

* String類型
	* " " 或者 ' ' 皆可
	* 每個字串符號幾乎都有一個toString方法, 唯獨 null以及undefined沒有
	* 若是數值, 可用toString(進制)來使用

	example:
	
		var num = 10; 
		alert(num.toString());         // "10" 
		alert(num.toString(2));        // "1010" 
		alert(num.toString(8));        // "12" 
		alert(num.toString(10));       // "10" 
		alert(num.toString(16));       // "a" 

 
* Object

		var o = new Object();

* Object有下列屬性與方法
	* constructor: 建構子
	* hasOwnProperty(propertyName): 用於檢查instance object是否具有propertyName的屬性 (不是檢查原型), 其中propertyName需要是字串型態
	* isPrototypeOf(object): 檢查object是否是傳入對象的類別原型
	* propertyIsEnumerable(propertyName): 檢查給定的屬性是否能夠使用for -in 敘述, propertyName需要是字串型態
	* toLocaleString(): 以當地環境返回字串型態
	* toString()
	* valueOf(): 返回適當的字串, Boolean或者是數值


* 數字位元操作符
	* ~ NOT
	 
			var num1 = 25;
			var num2 = ~num1;
			alert(num2); //-26
	* 基本上, ~ 操作, 若是變成負號, 就是取2的補數原則, 2的補數就是1的補數+1的結果, 所以25 => -(25+1) = -26
	* & AND (數字&的操作) 
	* | OR
	* ^ XOR (相同為0, 不同為1)
	* >> 有正負符號的右移
	* << 有正負符號的左移
	* >>> 無正負符號的右移 (對正數來說沒有差別, 對負數符號來說,會造成變成大正數)
	* <<< 無正負符號的左移

* Boolean的位元操作子
	* ! 反向
		* ! object, return false
		* ! ""(空字串) // true
		* ! "123" //true
		* !0 //true
		* ! 23(非0以及Infinity) //false
		* ! null / NaN / undefined //true
	* && 和C的&&相同, 但若有一個運算元不是布林, 那麼要遵守下列原則
		* 如果第一個運算元是Object, 則傳回第二個運算元
		* 若第二個運算元是Object, 則在第一個運算元求值的結果為true才return此object, else return false
		* 若兩個都object, 則return第二個object
		* 若某一運算元是 null, NaN或者undefined, 則返回nullm NaN或者undefined
	* && 屬於__短路操作__, 若第一個運算元是false, 就不會在求值下去
	* && 不能對尚未定義的變數操作, 會發生錯誤
	* || 或, 和C的||相同, 但若有一個運算元不是布林, 那麼要遵守下列原則
		* 如果第一個運算元是Object, 則傳回第一個運算元
		* 若第一個運算元求值結果為false, 則傳回第二個運算元
		* 若兩個運算元都是Object, 則return 第一個
		* 兩個運算元都是null, NaN或者undefined, 則返回null, NaN或者undefined
	* || 常用來避免賦予null or undefined, ECMAScript很常用, 舉個例子

			var myObject = preferredObject || backupObject;
			//如果preferredObject不是null, 則會assign給myObject, 如果是null, 則將backupObject給myObject

* 加+ 減- 乘* 除/ 取餘數% 和C語言相同


* 相等 == 不相等 !=
	* 若不是布林值, 則使用valueof轉換在判斷是否相等
	* null和undefined是相等
	* NaN不等於NaN

<p>
* 全等 === 和 不全等 !==
	* 不會經過隱性轉換的比較

	example
		
		var result1 = ("55" === 55) //false
		var result2 = ("55" !== 55) //true

		var result3 = ("55" == 55) //true
		var result4 = ("55" != 55) //false

		null == undefined //true
		null === undefined //false


* 三元運算子 記憶法: 變數 等於 判斷式 問號 真 冒號 假 =>結果 等於 判 問真 假冒

		variable = boolean_expression ? true_value : false_value; 


* 逗號(__,__)運算子: 可在一個敘述句裡執行多個操作

		var num1=1, num2=2, num3=3;

* 逗號可以用於賦值的時候, 只會傳回表達式中的最後一項

		var num = (5, 1, 4, 8, 0); // num 的值为 0 


* if , do while, while, for和C語言相同

* 由於 ECMAScript 中不存在塊級作用
域，因此在循環內部定義的變量也可以在外部訪問到

		var count = 10; 
		for (var i = 0; i < count; i++){
 			alert(i); 
		} 
		alert(i); //10


* for-in 敘述句
		
		Usage:
		for (property in expression) statement 
		
		Example:
		for (var propName in window) { 
     		document.write(propName); 
		} 
 
* 使用for-in之前, 都要check運算元不是null or undefined

* label 描述句, 用法 label: statement

		start: for (var i=0; i< count; i++){
			alert(i);
		}

* label通常用在break or continue, 需要和for搭配使用

* break和continue, 和C 相同

* break以及continue後可以接label, 若是break label, 代表跳出此label的敘述句,不再執行. continue label則是跳回此敘述句, 檢查是否再次進入



* with 描述句, with 語句的作用是將代碼的作用域設置到一個特定的對像中,

		with (expression) statement;
	
	example

 		var qs = location.search.substring(1); 
		var hostName = location.hostname; 
		var url = location.href;

	可換成

		with(location){ 
    		var qs = search.substring(1); 
    		var hostName = hostname; 
    		var url = href; 
		}

* __使用with會降低效能, 所以不建議使用__


  
* Switch, 和C相同
* 雖然 ECMAScript 中的 switch 語句借鑒自其他語​​言，但這個語句也有自己的特色。首先，可以在switch 語句中使用任何數據類型（在很多其他語言中只能使用數值），無論是字符串，還是Object都沒有問題。其次，每個 case 的值不一定是常量，可以是變量，甚至是表達式

		switch ("hello world") { 
    			case "hello" + " world":  
        			alert("Greeting was found."); 
        			break; 
			    case "goodbye":  
			        alert("Closing was found."); 
			        break; 
			    default:  
			        alert("Unexpected message was found."); 
		} 

* switch 語句在比較值時使用的是全等操作符，因此不會發生類型轉換（例如，字符串 "10" 不等於數值 10）


* 函數

		function functionName(arg0, arg1,...,argN) { 
    		statements 
		}

* ECMAScript 函數不介意傳遞進來多少個參數，也不在乎傳進來參數是什麼數據類型

* 也就是說, 即便你定義的函數只接受兩個參數,在調用這個函數時也未必一定要傳遞兩個參數。可以傳遞一個、三個甚至不傳遞參數, 而解析器永遠不會有什麼怨言。

* 原因是 ECMAScript 中的參數在內部是用一個數組來表示的。函數接收到的始終都是這個數組，而不關心數組中包含哪些參數（如果有參數的話）。如果這個數組中不包含任何元素，無所謂；如果包含多個元素，也沒有問題。實際上，在函數體內可以通過 __arguments__ 對象來訪問這個參數數組，從而獲取傳遞給函數的每一個參數。

* __arguments__ 對像只是與數組類似（它並不是 Array 的實例），因為可以使用方括號語法訪問它的每一個元素（即第一個元素是 __arguments[0]__，第二個元素是 __argumetns[1]__，以此類推），使用 __length__ 屬性來確定傳遞進來多少個參數。

		function sayHi() { 
    		alert("Hello " + arguments[0] + "," + arguments[1]); 
		}

 
* 這個事實說明了 ECMAScript 函數的一個重要特點：__命名的參數只提供便利，但不是必需的__。另外，在命名參數方面，其他語言可能需要事先創建一個函數簽名，而將來的調用必須與該簽名一致。但在 ECMAScript 中，沒有這些條條框框，解析器不會驗證命名參數。
 
* 通過訪問 arguments 對象的 length 屬性可以獲知有多少個參數傳遞給了函數。


		function howManyArgs() { 
    		alert(arguments.length); 
		} 
 
		howManyArgs("string", 45);  //2 
		howManyArgs();              //0 
		howManyArgs(12);            //1

 
* 另一個與參數相關的重要方面，就是 arguments 對象可以與命名參數一起使用 
 
* 關於 arguments 的行為，還有一點比較有意思。那就是它的值永遠與對應命名參數的值__保持同步__

		function doAdd(num1, num2) { 
    		arguments[1] = 10;     
    		alert(arguments[0] + num2); 
		} 

* 每次執行這個 doAdd() 函數都會重寫第二個參數，將第二個參數的值修改為 10。因為 arguments 對像中的值會自動反映到對應的命名參數，所以修改 arguments[1]，也就修改了 num2，結果它們的值都會變成 10。不過，這並不是說讀取這兩個值會訪問相同的內存空間；__它們的內存空間是獨立的，但它們的值會同步。__


* 另外還要記住，如果只傳入了一個參數，那麼為 arguments[1] 設置的值不會反應到命名參數中。這是因為 __arguments 對象的長度是由傳入的參數個數決定的，不是由定義函數時的命名參數的個數決定的。__

* 於參數還要記住最後一點：__沒有傳遞值的命名參數將自動被賦予 undefined 值。這就跟定義了變量但又沒有初始化一樣__

* 嚴格模式對如何使用 arguments 對像做出了一些限制。首先，像前面例子中那樣的賦值會變得無效。也就是說，即使把 arguments[1] 設置為 10，num2 的值仍然還是 undefined。其次，重寫 arguments 的值會導致語法錯誤（代碼將不會執行）。

* ECMAScript中的__所有參數傳遞的都是值__，不可能通過引用傳遞參數。也就是說都是call by value, 不是call by reference.

* ECMAScript 函數不能像傳統意義上那樣實現重載(OverLoading)
* 兩個相同名字的function, 後面的會覆寫前一個的定義


##變數, 作用域和內存問題##

* ECMAScript 中所有函数的参数都是按值传递的
* 有很多开发人员错误地认为：在局部作用域中修改的对象会在全局作用域中反映出来，就说明
参数是按引用传递的。为了证明对象是按值传递的, 我们再看一看下面这个经过修改的例子：

		function setName(obj) { 
    		obj.name = "Nicholas"; 
    		obj = new Object(); 
    		obj.name = "Greg"; 
		} 
 
		var person = new Object(); 
		setName(person); 
		alert(person.name);    //"Nicholas"

 
###檢測類型
* typeof 操作符是确定一个变量是字符串、数值、布尔值，还是 undefined 的最佳工具。如果变
量的值是一个对象或 null，则 typeof 操作符会像下面例子中所示的那样返回"object"

* 我们并不是想知道某个值是对象，而是想知道它是什么类型的对象。为此，ECMAScript 提供了 instanceof 操作符，其语法如下所示： 
 

		result = variable instanceof constructor 

		alert(person instanceof Object);  // 变量 person 是 Object 吗？ 
		alert(colors instanceof Array);   // 变量 colors 是 Array 吗？ 
		alert(pattern instanceof RegExp);   // 变量 pattern 是 RegExp 吗？

 
* 使用 typeof 操作符檢測函數時，該操作符會返回 "function"。在 Safari 5 及之前版本和 Chrome 7 及之前版本中使用 typeof 檢測正則表達式時，由於規範的原因，這個操作符也返回 "function"。 ECMA-262 規定任何在內部實現 [[Call]] 方法的對像都應該在應用 typeof 操作符時返回 "function"。由於上述瀏覽器中的正則表達式也實現了這個方法，因此對正則表達式應用 typeof 會返回 "function"。在
IE 和 Firefox 中，對正則表達式應用 typeof 會返回 "object"。

###執行環境以及作用域
* 在 Web 瀏覽器中，全局執行環境被認為是 window 對象，因此所有全局變量和函數都是作為 window 對象的屬性和方法創建的。某個執行環境中的所有代碼執行完畢後，該環境被銷毀，保存在其中的所有變量和函數定義也隨之銷毀（全局執行環境直到應用程序退出——例如關閉網頁或瀏覽器——時才會被銷毀）。

* 标识符解析是沿着作用域链一级一级地搜索标识符的过程。搜索过程始终从作用域链的前端开始，
然后逐级地向后回溯，直至找到标识符为止（如果找不到标识符，通常会导致错误发生）

* 内部环境可以通过作用域链访问所有的外部环境，但外部环境不能访问内部环境中的任何变量和函数。这些环境之间的联系是线性、有次序的。每个环境都可以向上搜索作用域链，以查询变量和函数名；但任何环境都不能通过向下搜索作用域链而进入另一个执行环境。

#### 沒有塊級的作用域
JavaScript 没有块级作用域经常会导致理解上的困惑。在其他类 C 的语言中，由花括号封闭的代码块都有自己的作用域（如果用 ECMAScript 的话来讲，就是它们自己的执行环境），因而支持根据条件来定义变量。

	if (true) { 
	    var color = "blue"; 
	} 
	 
	alert(color);    //"blue" 
 
这里是在一个 if 语句中定义了变量 color。如果是在 C、C++或 Java 中，color 会在 if 语句执行完毕后被销毁。但在 JavaScript 中，if 语句中的变量声明会将变量添加到当前的执行环境（在这里是全局环境）中。在使用 for 语句时尤其要牢记这一差异，例如： 
 
	for (var i=0; i < 10; i++){ 
	    doSomething(i); 
	} 
	 
	alert(i);      //10 
 
对于有块级作用域的语言来说，for 语句初始化变量的表达式所定义的变量，只会存在于循环的环境之中。而对于 JavaScript 来说，由 for 语句创建的变量 i 即使在 for 循环执行结束后，也依旧会存在
于循环外部的执行环境中。 

使用 var 声明的变量会自动被添加到最接近的环境中。在函数内部，最接近的环境就是函数的局部环境；在 with 语句中，最接近的环境是函数环境。如果初始化变量时没有使用 var 声明，该变量会自动被添加到全局环境

在编写 JavaScript 代码的过程中，不声明而直接初始化变量是一个常见的错误做法，因为这样可能会导致意外。我们建议在初始化变量之前，一定要先声明，这样就可以避免类似问题。在严格模式下，初始化未经声明的变量会导致错误。 

###管理內存

确保占用最少的内存可以让页面获得更好的性能。而优化内存占用的最佳方式，就是为执行中的代码只保存必要的数据。一旦数据不再有用，最好通过将其值设置为 null 来释放其引用——这个做法叫做解除引用（dereferencing）。这一做法适用于大多数全局变量和全局对象的属性。局部变量会在它们离开执行环境时自动被解除引用


##引用類型 (Reference Type)

引用類型的值（對象）是引用類型的一個實例。在 ECMAScript 中，引用類型是一種數據結構，用於將數據和功能組織在一起。它也常被稱為類，但這種稱呼並不妥當。儘管 ECMAScript從技術上講是一門面向對象的語言，但它不具備傳統的面向對象語言所支持的類和接口等基本結構。引用類型有時候也被稱為對象定義，因為它們描述的是一類對象所具有的屬性和方法。

虽然引用类型与类看起来相似，但它们并不是相同的概念。为避免混淆，我們不使用类这个概念

### Object Type

创建 Object 实例的方式有两种。第一种是使用 new 操作符后跟 Object 构造函数

	var person = new Object(); 
	person.name = "Nicholas"; 
	person.age = 29;


另一种方式是使用对象字面量表示法。对象字面量是对象定义的一种简写形式，目的在于简化创建
包含大量属性的对象的过程。

	var person = { 
	    name : "Nicholas", 
	    age : 29 
	}; 

在使用对象字面量语法时，属性名也可以使用字符串，如下面这个例子所示。

	var person = { 
	    "name" : "Nicholas", 
	    "age" : 29, 
	    5 : true 
	}; 

以上的5會自動轉換成字串的"5"

另外，使用对象字面量语法时，如果留空其花括号，则可以定义只包含默认属性和方法的对象，如
下所示： 
 
	var person = {};         //与 new Object()相同 
	person.name = "Nicholas"; 
	person.age = 29; 

虽然可以使用前面介绍的任何一种方法来定义对象，但开发人员更青睐对象字面量语法，因为这种语法要求的代码量少，而且能够给人封装数据的感觉。实际上，__对象字面量也是向函数传递大量可选参数的首选方式__


	function displayInfo(args) { 
	    var output = ""; 
	 
	    if (typeof args.name == "string"){ 
	 		output += "Name: " + args.name + "\n"; 
	    } 
	 
	    if (typeof args.age == "number") { 
	        output += "Age: " + args.age + "\n"; 
	    } 
	 
	    alert(output); 
	} 
	 
	displayInfo({  
	    name: "Nicholas",  
	    age: 29 
	}); 
	 
	displayInfo({ 
	    name: "Greg" 
	}); 

这种传递参数的模式最适合需要向函数传入大量可选参数的情形。一般来讲，命名参数虽然容易处理，但在有多个可选参数的情况下就会显示不够灵活。最好的做法是对那些必需值使用命名参数，而使用对象字面量来封装多个可选参数。

一般来说，访问对象属性时使用的都是__点表示法__，这也是很多面向对象语言中通用的语法。不过，在 JavaScript 也可以使用__方括号__表示法来访问对象的属性。在__使用方括号语法__时，应该将要访问的属性以__字符串__的形式放在方括号中，

	alert(person["name"]);        //"Nicholas" 
	alert(person.name);          //"Nicholas" 
 
从功能上看，这两种访问对象属性的方法没有任何区别。但方括号语法的主要优点是可以通过变量
来访问属性，例如： 
 
	var propertyName = "name"; 
	alert(person[propertyName]);   //"Nicholas" 
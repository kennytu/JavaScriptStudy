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

* 原因是 ECMAScript 中的參數在內部是用一個陣列來表示的。函數接收到的始終都是這個陣列，而不關心陣列中包含哪些參數（如果有參數的話）。如果這個陣列中不包含任何元素，無所謂；如果包含多個元素，也沒有問題。實際上，在函數體內可以通過 __arguments__ 對象來訪問這個參數陣列，從而獲取傳遞給函數的每一個參數。

* __arguments__ 對像只是與陣列類似（它並不是 Array 的實例），因為可以使用方括號語法訪問它的每一個元素（即第一個元素是 __arguments[0]__，第二個元素是 __argumetns[1]__，以此類推），使用 __length__ 屬性來確定傳遞進來多少個參數。

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

	person["first name"] = "Nicholas"; 
 
由于"first name"中包含一个空格，所以不能使用点表示法来访问它。然而，__属性名中是可以包含非字母非数字的__，这时候就可以__使用方括号表示法来访问它们__。

通常，除非必须使用变量来访问属性，否则我们建议使用点表示法。

### Array Type 

	var colors = new Array(); 
	var colors = new Array(20); 
	var colors = new Array("red", "blue", "green");

给构造函数传递一个值也可以创建陣列。但这时候问题就复杂一点了，因为如果传递的__是数值，则会按照该数值创建包含给定项数的陣列__；而如果传递的是__其他类型的参数，则会创建包含那个值的只有一项的陣列__。下面就两个例子： 
 
	var colors = new Array(3);        // 创建一个包含 3 项的陣列 
	var names = new Array("Greg");      // 创建一个包含 1 项，即字符串"Greg"的陣列

在使用 Array 构造函数时也可以省略 new 操作符。如下面的例子所示，省略 new 操作符的结果相同： 
 
	var colors = Array(3);         // 创建一个包含 3 项的陣列 
	var names = Array("Greg");     // 创建一个包含 1 项，即字符串"Greg"的陣列  

建陣列的第二种基本方式是使用陣列字面量表示法。陣列字面量由一对包含陣列项的方括号表示，多个陣列项之间以逗号隔开
	
	var colors = ["red", "blue", "green"];  // 创建一个包含 3 个字符串的陣列 
	var names = [];                       // 创建一个空陣列 
	var values = [1,2,];                   // 不要这样！这样会创建一个包含 2 或 3 项的陣列 
	var options = [,,,,,];                 // 不要这样！这样会创建一个包含 5 或 6 项的陣列 

在像这种省略值的情况下，每一项都将获得 undefined 值；这个结果与调用 Array 构造函数时传递项数在逻辑上是相同的。但是由于 IE 的实现与其他浏览器不一致我们强烈建议不要使用这种语法(第二種但是省略語法, 一些瀏覽器會有bug)

讀取:
	
	var colors = ["red", "blue", "green"];  // 定义一个字符串陣列 
	alert(colors[0]);                     // 显示第一项 
	colors[2] = "black";                   // 修改第三项 
	colors[3] = "brown";                   // 新增第四项

陣列的 length 属性很有特点——它不是只读的。因此，通过设置这个属性，可以从陣列的末尾移除项或向陣列中添加新项。请看下面的例子： 
 
	var colors = ["red", "blue", "green"];     // 创建一个包含 3 个字符串的陣列 
	colors.length = 2; 
	alert(colors[2]);                 //undefined 

利用 length 属性也可以方便地在陣列末尾添加新项，如下所示：

	var colors = ["red", "blue", "green"];     // 创建一个包含 3 个字符串的陣列 
	colors[colors.length] = "black";            //（在位置 3）添加一种颜色 
	colors[colors.length] = "brown";            //（在位置 4）再添加一种颜色 

插入99

	var colors = ["red", "blue", "green"];      // 创建一个包含 3 个字符串的陣列 
	colors[99] = "black";                     // （在位置 99）添加一种颜色 
	alert(colors.length); // 100

 在这个例子中，我们向 colors 陣列的位置 99 插入了一个值，结果陣列新长度（length）就是 100（99+1）。而位置 3 到位置 98 实际上都是不存在的，所以访问它们都将返回 __undefined__。

###檢測陣列

自从 ECMAScript 3 做出规定以后，就出现了确定某个对象是不是数组的经典问题。对于一个网页,或者一个全局作用域而言，使用 instanceof 操作符就能得到满意的结果： 
	 
	if (value instanceof Array){  
	    //对数组执行某些操作 
	} 
 
instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的 Array 构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。

为了解决这个问题，ECMAScript 5 新增了 __Array.isArray()__方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的。这个方法的用法如下。 
 
	if (Array.isArray(value)){ 
	    //对数组执行某些操作 
	} 
 
支持 Array.isArray()方法的浏览器有 IE9+、Firefox 4+、Safari 5+、Opera 10.5+和 Chrome

###轉換方法

所有对象都具有 toLocaleString()、toString()和 valueOf()方法。其中，调用数组的 toString()方法会返回__由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串__。而调用__valueOf()返回的还是数组__。实际上，为了创建这个字符串会调用数组每一项的 toString()方法。来看下面这个例子。 
 
	var colors = ["red", "blue", "green"];     // 创建一个包含 3 个字符串的数组 
	alert(colors.toString());     // red,blue,green 
	alert(colors.valueOf());      // red,blue,green 
	alert(colors);                // red,blue,green 

呼叫toLocaleString寫法:

	var person1 = { 
	    toLocaleString : function () { 
	        return "Nikolaos"; 
	    }, 
	     
	    toString : function() { 
	        return "Nicholas"; 
	    } 
	}; 
	 
	var person2 = { 
	    toLocaleString : function () { 
	        return "Grigorios"; 
	    }, 
	     
	    toString : function() { 
	        return "Greg"; 
	    } 
	}; 
	 
	var people = [person1, person2]; 
	alert(people);                        //Nicholas,Greg 
	alert(people.toString());               //Nicholas,Greg 
	alert(people.toLocaleString());         //Nikolaos,Grigorios 


join()方法只接收一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串。请看下面的例子： 
 
	var colors = ["red", "green", "blue"]; 
	alert(colors.join(","));       //red,green,blue 
	alert(colors.join("||"));      //red||green||blue 

如果不给 join()方法传入任何值，或者给它传入 undefined，则使用逗号作为分隔符

如果数组中的某一项的值是 null 或者 undefined，那么该值在 join()、toLocaleString()、toString()和 valueOf()方法返回的结果中以空字符串表示。

###Stack Methods
数组可以表现得就像栈一样，后者是一种可以限制插入和删除项的数据结构。栈是一种 LIFO（Last-In-First-Out，
后进先出）的数据结构，也就是最新添加的项最早被移除。而栈中项的插入（叫做推入）和移除（叫做弹出），只发生在一个位置——栈的顶部。ECMAScript 为数组专门提供了 push()和 pop()方法，以便实现类似栈的行为。

	var colors = new Array();                   // 创建一个数组 
	var count = colors.push("red", "green");    // 推入两项 
	alert(count);    //2 
	 
	count = colors.push("black");               // 推入另一项 
	alert(count);     //3 
	 
	var item = colors.pop();                   // 取得最后一项 
	alert(item);      //"black" 
	alert(colors.length);   //2 
	
	var colors = ["red", "blue"]; 
	colors.push("brown");               // 添加另一项 
	colors[3] = "black";                // 添加一项 
	alert(colors.length);    // 4 
	 
	var item = colors.pop();            // 取得最后一项 
	alert(item);  //"black" 

### Queue Methods
队列数据结构的访问规则是 FIFO（First-In-First-Out,先进先出）
push() / shift() / unshift()

	var colors = new Array();                   //创建一个数组 
	var count = colors.push("red", "green");    //推入两项 
	alert(count);    //2 
	 
	count = colors.push("black");               //推入另一项 
	alert(count);     //3 
	 
	var item = colors.shift();                  //取得第一项 
	alert(item);      //"red" 
	alert(colors.length); //2 
 
注意pop()是移除陣列最後一項

	count = colors.unshift("black");                 //推入另一项 
	alert(count);   //3 
	 
	var item = colors.pop();                        //取得最后一项 
	alert(item);    //"green" 
	alert(colors.length); //2 

这个例子创建了一个数组并使用 unshift()方法先后推入了 3 个值。首先是"red"和"green"，然后是"black"，数组中各项的顺序为"black"、"red"、"green"。在调用 pop()方法时，移除并返回的是最后一项，即"green"。

### Reordering Methods

reverse() and sort().
sort()方法可以接收一个比较函数作为参数，以便我们指定哪个值位于哪个值的前面。

	function compare(value1, value2) { 
	    if (value1 < value2) { 
	        return -1; 
	    } else if (value1 > value2) { 
	        return 1; 
	    } else { 
	        return 0; 
	    } 
	} 

	var values = [0, 1, 5, 10, 15]; 
	values.sort(compare); 
	alert(values);   //0,1,5,10,15 

reverse()和 sort()方法的返回值是经过排序之后的陣列


### 操作方法 Manipulation Methods

concat()方法可以基于当前数组中的所有项创建一个新数组。具体来说，这个方法会先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。在没有给 concat()方法传递参数的情况下，它只是复制当前数组并返回副本。如果传递给 concat()方法的是一或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中。如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾。

	var colors = ["red", "green", "blue"]; 
	var colors2 = colors.concat("yellow", ["black", "brown"]); 
	 
	alert(colors);     //red,green,blue         
	alert(colors2);    //red,green,blue,yellow,black,brown 

slice()，它能够基于当前数组中的一或多个项创建一个新数组。slice()方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下，slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项。注意，slice()方法不会影响原始数组

	var colors = ["red", "green", "blue", "yellow", "purple"]; 
	var colors2 = colors.slice(1); 
	var colors3 = colors.slice(1,4); 
	 
	alert(colors2);   //green,blue,yellow,purple 
	alert(colors3);   //green,blue,yellow 


splice()方法，这个方法恐怕要算是最强大的数组方法了，它有很多种用法。
splice()的主要用途是向数组的中部插入项，但使用这种方法的方式则有如下 3 种。 

* 删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。例如，splice(0,2)会删除数组中的前两项。 
* 插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、0（要删除的项数和要插入的项。如果要插入多个项，可以再传入第四、第五，以至任意多个项。例如，splice(2,0,"red","green")会从当前数组的位置 2 开始插入字符串"red"和"green"。 
* 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。例如，splice (2,1,"red","green")会删除当前数组位置 2 的项，然后再从位置 2 开始插入字符串"red"和"green"。 

splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）。


### 位置方法 Location Methods 

indexOf()和 lastIndexOf()。这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中，indexOf()方法从数组的开头（位置 0）开始向后查找，lastIndexOf()方法则从数组的末尾开始向前查找

这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回-1

在比较第一个参数与数组中的每一项时，会使用全等操作符；也就是说，要求查找的项必须严格相等


### 迭代方法 Iterative Methods

ECMAScript 5 为数组定义了 5 个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象——影响 this 的值。

传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响方法的返回值。以下是这 5 个迭代方法的作用。
 
* every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回true。 
* filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。 
* forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。 
* map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。 
* some()：对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true。
 
以上方法都不会修改数组中的包含的值。 
在这些方法中，最相似的是 every()和 some()，它们都用于查询数组中的项是否满足某个条件。

* 对 every()来说，传入的函数必须对每一项都返回 true，这个方法才返回 true；否则，它就返回false。
* 而 some()方法则是只要传入的函数对数组中的某一项返回 true，就会返回 true。


		var numbers = [1,2,3,4,5,4,3,2,1]; 
		 
		var everyResult = numbers.every(function(item, index, array){ 
		    return (item > 2);  
		}); 
		 
		alert(everyResult);     //false 
		 
		var someResult = numbers.some(function(item, index, array){ 
		    return (item > 2); 
		}); 
		 
		alert(someResult);      //true 



filter()函数，它利用指定的函数确定是否在返回的数组中包含某一项。例如，要
返回一个所有数值都大于 2 的数组，可以使用以下代码。 
	var numbers = [1,2,3,4,5,4,3,2,1]; 
	 
	var filterResult = numbers.filter(function(item, index, array){ 
	    return (item > 2); 
	}); 
	 
	alert(filterResult);    //[3,4,5,4,3] 


map()也返回一个数组，而这个数组的每一项都是在原始数组中的对应项上运行传入函数的结果。例如，可以给数组中的每一项乘以 2，然后返回这些乘积组成的数组，如下所示。 

	var numbers = [1,2,3,4,5,4,3,2,1]; 
	 
	var mapResult = numbers.map(function(item, index, array){ 
	    return item * 2; 
	}); 
	 
	alert(mapResult);  //[2,4,6,8,10,8,6,4,2] 

forEach()，它只是对数组中的每一项运行传入的函数。这个方法没有返回值
本质上与使用 for 循环迭代数组一样。来看一个例子。 

	var numbers = [1,2,3,4,5,4,3,2,1];
	numbers.forEach(function(item, index, array){ 
	    //执行某些操作  
	}); 


### 歸併方法 Reduction Methods

ECMAScript  5 还新增了两个归并数组的方法：reduce()和 reduceRight()。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。其中，reduce()方法从数组的第一项开始，逐个遍历到最后。而 reduceRight()则从数组的最后一项开始，向前遍历到第一项。

这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为归并基础的初始值. 
传给 reduce()和 reduceRight()的函数接收 4 个参数：前一个值、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。

使用 reduce()方法可以执行求数组中所有值之和的操作，比如： 

	var values = [1,2,3,4,5]; 
	var sum = values.reduce(function(prev, cur, index, array){ 
	    return prev + cur;  
	}); 
	alert(sum); //15 
 
第一次执行回调函数，prev 是 1，cur 是 2。第二次，prev 是 3（1 加 2 的结果），cur 是 3（数组的第三项）。这个过程会持续到把数组中的每一项都访问一遍，最后返回结果


### Date Type

var now = new Date();

ECMAScript 5 添加了 Data.now()方法，返回表示调用这个方法时的日期和时间的毫秒数。这个方法简化了使用 Data 对象分析代码的工作。例如： 
 
	//取得开始时间 
	var start = Date.now(); 
	 
	//调用函数 
	doSomething(); 
	 
	//取得停止时间 
	var stop = Date.now(), 
	    result = stop – start; 
 
支持 Data.now()方法的浏览器包括 IE9+、Firefox  3+、Safari  3+、Opera  10.5 和 Chrome。在不支持它的浏览器中，__使用+操作符把 Data 对象转换成字符串__，也可以达到同样的目的。 
 
	//取得开始时间 
	var start = +new Date(); 
	 
	//调用函数 
	doSomething(); 
	//取得停止时间 
	var stop = +new Date(), 
	result = stop - start; 


### Date-Formatting Methods

Date 类型还有一些专门用于将日期格式化为字符串的方法，这些方法如下。
 
* toDateString()——以特定于实现的格式显示星期几、月、日和年； 
* toTimeString()——以特定于实现的格式显示时、分、秒和时区； 
* toLocaleDateString()——以特定于地区的格式显示星期几、月、日和年； 
* toLocaleTimeString()——以特定于实现的格式显示时、分、秒； 
* toUTCString()——以特定于实现的格式完整的 UTC 日期。 

与 toLocaleString()和 toString()方法一样，以上这些字符串格式方法的输出也是因浏览器而异的，因此没有哪一个方法能够用来在用户界面中显示一致的日期信息。


### 日期/时间组件方法 Date/Time Component Methods

- getTime()  返回表示日期的毫秒数；与valueOf()方法返回的值相同 
- setTime(毫秒)  以毫秒数设置日期，会改变整个日期 
- getFullYear()  取得4位数的年份（如2007而非仅07） 
- getUTCFullYear()  返回UTC日期的4位数年份 
- setFullYear(年)  设置日期的年份。传入的年份值必须是4位数字（如2007而非仅07） 
- setUTCFullYear(年)  设置UTC日期的年份。传入的年份值必须是4位数字（如2007而非仅07） 
- getMonth()  返回日期中的月份，其中0表示一月，11表示十二月 
- getUTCMonth()  返回UTC日期中的月份，其中0表示一月，11表示十二月 
- setMonth(月)  设置日期的月份。传入的月份值必须大于0，超过11则增加年份 
- setUTCMonth(月)  设置UTC日期的月份。传入的月份值必须大于0，超过11则增加年份 
- getDate()  返回日期月份中的天数（1到31） 
- getUTCDate()  返回UTC日期月份中的天数（1到31） 
- setDate(日)  设置日期月份中的天数。如果传入的值超过了该月中应有的天数，则增加月份 
- setUTCDate(日)  设置UTC日期月份中的天数。如果传入的值超过了该月中应有的天数，则增加月份 
- getDay()  返回日期中星期的星期几（其中0表示星期日，6表示星期六） 
- getUTCDay()  返回UTC日期中星期的星期几（其中0表示星期日，6表示星期六） 
- getHours()  返回日期中的小时数（0到23） 
- getUTCHours()  返回UTC日期中的小时数（0到23） 
- setHours(时)  设置日期中的小时数。传入的值超过了23则增加月份中的天数 
- setUTCHours(时)  设置UTC日期中的小时数。传入的值超过了23则增加月份中的天数 
- getMinutes()  返回日期中的分钟数（0到59） 
- getUTCMinutes()  返回UTC日期中的分钟数（0到59） 
- setMinutes(分)  设置日期中的分钟数。传入的值超过59则增加小时数 
- setUTCMinutes(分)  设置UTC日期中的分钟数。传入的值超过59则增加小时数 
- getSeconds()  返回日期中的秒数（0到59） 
- getUTCSeconds()  返回UTC日期中的秒数（0到59） 
- setSeconds(秒)  设置日期中的秒数。传入的值超过了59会增加分钟数 
- setUTCSeconds(秒)  设置UTC日期中的秒数。传入的值超过了59会增加分钟数 
- getMilliseconds()  返回日期中的毫秒数 
- getUTCMilliseconds()  返回UTC日期中的毫秒数 
- setMilliseconds(毫秒)  设置日期中的毫秒数 
- setUTCMilliseconds(毫秒)  设置UTC日期中的毫秒数 
- getTimezoneOffset()  返回本地时间与UTC时间相差的分钟数。例如，美国东部标准时间返回300。在某地进入夏令时的情况下，这个值会有所变化


### RegExp Type

先跳過


### Function Type (重頭戲)




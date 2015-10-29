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

* 
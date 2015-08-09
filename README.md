# javascript best practices

- 三目运算符

  常规代码:
  
  		var authorized = false;
  		var active;
  		
  		if(authorized) {
  		  active = true;
  		} else {
  		  active = false;
  		}  
  		
  		
  好的实践:
  
  		var active = authorized ? true : false;
  		
  注: 三目运算符始终会返回一个结果。条件判断，除了false, 0, undefined, NaN, "", null,其它的都为true。
  
  延伸:
  
        //执行函数
  		authorized ? function(){
  		               console.log('user is active...');
  		             }()
  		           : function(){
  		               console.log('user is not active...');
  		             }();
  		             
  		//多个表达式             
  	    var a,b;
  	    authorized ? (a = 1, b = 2) : (a = b = 0);
  	    
  	    //嵌套
  	    var c; 
  	    authorized ? (a = 1, b = 2) : authorized ? c = 3 : c = 0;
  
  
- 使用条件||和&&

  常规代码:
  
  		var class = {
  		  _addMember: function(member){
  		    this.members = this.members ? this.members : [];
  		    this.members.push(member);
  		  }
  		};
  		
  好的实践:
  
  		var class = {
  		  _addMember: function(member){
  		    this.members = this.members || [];
  		    this.members.push(member);
  		  }
  		}
  		
  注: 这里主要注意||操作符前面表达式得出的结果是true还是false, true的话，执行短路操作，也就是碰到第一个表达式true的就返回。如果是&&的话，一直要判断到最后才能确定最终表达式的值。
  
- switch语句使用

  常规代码:
  
  		function findKindVal(kind){
  		  if(kind == 'a') {
  		    return 0;
  		  } else if(kind == 'b') {
  		    return 1;
  		  } else if(kind == 'c') {
  		  	return 2;
  		  }...
  		}
  		
  好的实践:
  
  		function findKindVal(kind) {
  		  switch(kind) {
  		  	case 'a':
  		  	  return 0;
  		  	case 'b':
  		  	  return 1;
  		  	case 'c':
  		  	  return 2;
  		  	case 'd':
  		  	case 'e':
  		  	  return 3;
  		  	default:
  		  	  return '-1';
  		  }
  		}
  		
  注: 这里是直接return了，如果不是的话，需要加上break中断条件判断。这里可以把一些命中率高的选项放在前面。
  
- 优化循环

  常规代码:
  
  		var tasks = {
  		  numbers: [1,2,3,4,5,6,7,8,9]
  		};
  		
  		for(var i = 0; i < tasks.numbers.length; i++) {
  		  console.log(tasks.numbers[i]);
  		}
  		
  好的实践:
  
  		var numbers = tasks.numbers,
     		len = numbers.length;
     		
  		for(var i = 0; i < len; i++){
  		  console.log(numbers[i])
  		}
  		
  		//或者
  		var i = len;
  		while(i--){
  		  console.log(numbers[len - (i + 1)]);
  		}

  注: 这里要访问i, numbers, length, 数组索引[i],效率会低一些，和0的比较效率是最高的。
  
  
- 执行脚本

  常规代码:
  
  		<head>
  		  <script src="..."></script>
  		  ...
  		</head>
  		<body>
  		  <script src="..."></script>
  		  //显示页面内容
  		</body>
  		
  问题: 如果脚本执行的业务逻辑过多，会导致页面内容无法立刻呈现在用户面前，这里应该将页面在显示给用户之前需要处理的业务逻辑，放在页面加载前处理，之后的放在底部。或者使用HTML5的async属性允许页面显示在脚本运行前。
  
  好的实践 1:
  
  		<body>
  		//显示页面内容
  		<script src="..."><script>
  		</body>
  		
  好的实践 2:
  
  		<head>
  		  <script src="..." async></script>
  		</head>
  		//...
  
- 使用继承高效使用内存

  使一类对象共有的方法都使用构造器原型。每个对象都共用方法，而各自特有的属性，在实例化之后可以自定义。

  常规代码:
  
  		function ObjectA () {
  		  this.methodA = function(){}
  		  this.methodB = function(){}
  		}
  		
  		var objecta = new ObjectA();
  		
  
  好的实践:
  
  		ObjectA.prototype = {
  		  methodA: function(){},
  		  methodB: function(){}
  		};
  		
- 使用createDocumentFragment添加DOM

  页面添加DOM常规做法是获取页面DOM节点，然后添加新的DOM。每一次添加DOM都会刷新页面，消耗时间而且降低效率。使用createDocumentFragment方法将新节点添加到一个fragment state上，最后将fragment上的所有节点一次性添加到页面DOM上。
  
  
  常规代码: 
  
      var list = document.getElementById('book_list');
      for(var i = 0; i < 10; i++) {
        var element = document.createElement('li');
        element.appendChild(document.createTextNode('book_' + i));
        list.appendChild(element);
      }


   好的实践:
   
      var list = document.getElementById('book_list');
      var fragment = document.createDocumentFragment();
      
      for(var i = 0; i < 10; i++) {
        var element = document.createElement('li');
        element.appendChild(document.createTextNode('book_' + i));
        fragment.appendChild(element);
      }
      
      list.appendChild(fragment);
      
      

  		  		  

 


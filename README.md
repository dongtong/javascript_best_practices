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
  		
  		
  最佳实践:
  
  		var active = authorized ? true : false;
  		
  注:
  
  三目运算符始终会返回一个结果。条件判断，除了false, 0, undefined, NaN, "", null,其它的都为true。
  
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
  
 


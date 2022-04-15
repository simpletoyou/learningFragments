es6语法

[阮一峰 es6入门 ](https://www.yuque.com/ostwind/es6/docs-destructuring)

1. 解构赋值

2. 函数参数解构赋值
		
		function add([x, y]){
		  return x + y;
		}
		
		add([1, 2]); // 3
		
		上述代码中，函数add的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量x和y。对于函数内部的代码来说，它们能感受到的参数就是x和y。
		
		[[1, 2], [3, 4]].map(([a, b]) => a + b);
		// [ 3, 7 ]
		
		function move({x = 0, y = 0} = {}) {
		  return [x, y];
		}
		
		函数参数的解构赋值也可以使用默认值
		
		move({x: 3, y: 8}); // [3, 8]
		move({x: 3}); // [3, 0]
		move({}); // [0, 0]
		move(); // [0, 0]
		
		上面代码中，函数move的参数是一个对象，通过对这个对象进行解构，得到变量x和y的值。如果解构失败，x和y等于默认值。
		
		注意，下面的写法会得到不一样的结果。
		
		function move({x, y} = { x: 0, y: 0 }) {
		  return [x, y];
		}
		move({x: 3, y: 8}); // [3, 8]
		move({x: 3}); // [3, undefined]
		move({}); // [undefined, undefined]
		move(); // [0, 0]
		
		上面代码是为函数move的参数指定默认值，而不是为变量x和y指定默认值，所以会得到与前一种写法不同的结果。
		undefined就会触发函数参数的默认值。
		
		[1, undefined, 3].map((x = 'yes') => x);
		// [ 1, 'yes', 3 ]
		
		用途
		变量的解构赋值用途很多。
		
		（1）交换变量的值
		
		let x = 1;
		let y = 2;
		[x, y] = [y, x];
		
		上面代码交换变量x和y的值，这样的写法不仅简洁，而且易读，语义非常清晰。
		
		（2）从函数返回多个值
		
		函数只能返回一个值，如果要返回多个值，只能将它们放在数组或对象里返回。有了解构赋值，取出这些值就非常方便。
		
		// 返回一个数组
		function example() {
		  return [1, 2, 3];
		}
		let [a, b, c] = example();
		
		// 返回一个对象
		function example() {
		  return {
		    foo: 1,
		    bar: 2
		  };
		}
		
		let { foo, bar } = example();
		
		（3）函数参数的定义
		
		解构赋值可以方便地将一组参数与变量名对应起来。
		
		// 参数是一组有次序的值
		function f([x, y, z]) { ... }
		f([1, 2, 3]);
		
		// 参数是一组无次序的值
		function f({x, y, z}) { ... }
		f({z: 3, y: 2, x: 1});
		
		（4）提取 JSON 数据
		
		解构赋值对提取 JSON 对象中的数据，尤其有用。
		
		let jsonData = {
		  id: 42,
		  status: "OK",
		  data: [867, 5309]
		};
		
		let { id, status, data: number } = jsonData;
		console.log(id, status, number);
		// 42, "OK", [867, 5309]
		
		上面代码可以快速提取 JSON 数据的值。
		
		（5）函数参数的默认值
		
		jQuery.ajax = function (url, {
		  async = true,
		  beforeSend = function () {},
		  cache = true,
		  complete = function () {},
		  crossDomain = false,
		  global = true,
		  // ... more config
		} = {}) {
		  // ... do stuff
		};
		
		指定参数的默认值，就避免了在函数体内部再写var foo = config.foo || 'default foo';这样的语句。
		
		（6）遍历 Map 结构
		
		任何部署了 Iterator 接口的对象，都可以用for...of循环遍历。Map 结构原生支持 Iterator 接口，配合变量的解构赋值，获取键名和键值就非常方便。
		
		const map = new Map();
		map.set('first', 'hello');
		map.set('second', 'world');
		for (let [key, value] of map) {
		  console.log(key + " is " + value);
		}
		// first is hello
		// second is world
		
		如果只想获取键名，或者只想获取键值，可以写成下面这样。
		
		// 获取键名
		for (let [key] of map) {
		  // ...
		}
		
		// 获取键值
		for (let [,value] of map) {
		  // ...
		}
		（7）输入模块的指定方法
		
		加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。
		const { SourceMapConsumer, SourceNode } = require("source-map");
		
		

3. ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。

4. includes(), startsWith(), endsWith()
	传统上，JavaScript 只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。
	• includes()：返回布尔值，表示是否找到了参数字符串。
	• startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
	• endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
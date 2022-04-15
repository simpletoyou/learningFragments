less（开发模式下使用Less）

直接在html页面引用.less文件，然后借助less.js去编译less文件动态生成css样式而存在于当前页面，这种方式适用于开发模式。

（1）Less里面的变量都是以@作为变量的起始标识，变量名由字母、数字、_和-组成；
（2）在一个文件里面定义的同名变量存在全局变量和局部变量的区别

1、less中变量的使用；

	在less，允许我们使用以变量的形式来定义，定义方式：@k:v; 使用方式：@k;
	
	<div class="box"></div>
	 
	<style lang="less">
	@color:red;
	@k:100px;
	.box{
	width:@k;
	height:@k;
	background: @color;
	}
	</style>
	

2、字符串拼接变量使用方式；

	<div class="box1"></div>
	 
	<style lang="less" scoped>
	@img:'./img/';
	@k:100px;
	.box1{
			width:@k;
			height:@k;
			background:url("@{img}1.png")
	}
	</style>

3、多层嵌套+变量计算；

	<div class="box1">
			<div class="box2">
					<div class="box3"></div>
			</div>
	</div>
	 
	<style lang="less">
	@k:100px;
	 .box1{
			 width: @k;
			 height:@k;
			 background: red;
			 .box2{
					 width: @k/2;
					 height:@k/2;
					 background: green;
					 .box3{
							 width: @k/3;
							 height:@k/3;
							 background: blue;
					 }
			 }
	 }
	</style>

4、混合 = 函数

	<div class="box1">我是box1</div>
	<div class="box2">我是box2</div>
	 
	<style lang="less">
	//定义一个函数；
	.test(@color:red,@size:14px){
			background: @color;
			font-size:@size;
	}
	.box1{
	//  不传参，使用默认的；
			.test()
	}
	.box2{
	//  给函数传参；
			.test(@color:green,@size:30px)
	}
	</style>


5、匹配模式

	<div class="box"></div>
	//定义的css
	<style lang="less">
	.sjx(@_,@color,@size){
			width: 0;
			height:0;
			border:@size solid @color;
			border-color:transparent;
	}
	//左边三角形
	.sjx(l,@color,@size){
			border-left-color:@color;
	}
	//上边三角形
	.sjx(t,@color,@size){
			border-top-color:@color;
	}
	//右边三角形
	.sjx(r,@color,@size){
			border-right-color:@color;
	}
	//左边三角形
	.sjx(b,@color,@size){
			border-bottom-color:@color;
	}
	//这里匹配调用
	.box{
			.sjx(r,red,20px)
	}
	</style>

7、颜色函数

	<p>默认红色</p>
	<p>默认绿色</p>
	<ul>
			<li <li v-for="i in 6">测试</li>
	</ul>
	<span>混合</span>
	 
	<style lang="less" scoped>
			*{
					padding: 0;
					margin: 0;
			}
			@color:red;
			@color1:green;
			p:nth-child(1){
					background: @color;
			};
			 p:nth-child(2){
					background: @color1;
			};
			ul{
					list-style: none;
							li:nth-child(1){
							background:lighten(@color,50%);
					}
							li:nth-child(2){
							background:darken(@color,50%);
					}
							li:nth-child(3){
							background:saturate(@color,50%);
					}
							li:nth-child(4){
							background:desaturate(@color,50%);
					}
							li:nth-child(5){
							background:spin(@color,50%);
					}
							li:nth-child(6){
							background:spin(@color,50%);
					}
			}
			span{
					background: mix(@color,@color1);
			}
	</style>


8、运算符

        可以对高度、宽度、角度进行计算；

	<ul>
			<li v-for="item in 4">{{item}}</li>
	</ul>
	<style lang="less" scoped>
		@k:10px;
			ul{
					list-style: none;
						 li{
								 border:1px solid ;
								 margin:10px 0 ;
						 }
							li:nth-child(1){
									width: @k + @k;
									height:@k;
							}
							li:nth-child(2){
									width: @k -5px;
									height:@k;
							}
							li:nth-child(3){
									width: @k * @k;
									height:@k;
							}
							li:nth-child(4){
									width: @k / 2;;
									height:@k;
							}
			}
	</style>
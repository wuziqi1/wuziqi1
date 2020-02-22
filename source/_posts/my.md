---
title: 关于IOS下 底部fixed 
---
#### 关于IOS下 底部fixed 里面有个input框 弹出软键盘的遮住input的问题，安卓下展现的效果还是比较好的，但是苹果下，有的飞走了，有的挡住了，比较蛋疼，而且JS没有办法操作软件的事件，这可难坏我了。于是各种搜度娘。网上的办法很多例子都不怎么管用。
![布局基本这样](http://upload-images.jianshu.io/upload_images/3957512-6e4a437e3e0cafcb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



废话不说了 直接上代码

css布局
```xml
                    
			* {
				margin: 0;
				padding: 0;
			}
			
			header {
				position: absolute;
				top: 0;
				left: 0;
				z-index: 9999;
				width: 100%;
				height: 50px;
				line-height: 50px;
				font-size: 18px;
				text-align: center;
				background: #ccc;
			}
			
			main {
				position: absolute;
				top: 50px;
				bottom: 0;
				width: 100%;
				margin-bottom: 50px;
				overflow-y: scroll;
				/*让滑动更流畅*/
				-webkit-overflow-scrolling: touch;
			}
			
			footer {
				position: absolute;
				bottom: 0;
				left: 0;
				width: 100%;
				height: 50px;
				line-height: 50px;
				text-align: center;
				background: #666;
				border-top: 1px solid #e6e6e6;
			}
			
			footer input {
				display: inline-block;
				width: 90%;
				height: 20px;
				font-size: 14px;
				outline: none;
				border: 1px solid #e6e6e6;
				border-radius: 5px;
			}
```
html
```xml
                <header>
			header
		</header>
		<main>
			<ul>

				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li>
				<li>14</li>
				<li>15</li>
				<li>16</li>
				<li>17</li>
				<li>18</li>
				<li>19</li>
				<li>20</li>
				<li>1</li>
				<li>12</li>
				<li>13</li </ul>
		</main>
		<footer>
			<input type="text" placeholder="Type here...">
		</footer>
```
js
```xml
       <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
		<script src="https://cdn.bootcss.com/fastclick/1.0.6/fastclick.min.js"></script>
		<script type="text/javascript">
			$(function() {
				FastClick.attach(document.body);
				var topValue = 0,
					interval = null;
				document.querySelector('main').onscroll = function() {
					if(interval == null) {

						interval = setInterval(function() {
							if(document.documentElement.scrollTop == topValue) {

								$('input').on('focus', function() {

									var target = this;
									clearInterval(timer);

									timer = setInterval(function() {
										target.scrollIntoView(true);
									}, 100);
								});

								clearInterval(interval);
								interval = null;
							}else{
								$('input').unbind('click')
							}
						}, 400);
					}
					topValue = document.documentElement.scrollTop;
				}

				var timer = null;

			})
		</script>
```
####但是还有个问题  就是滑动到最上面的时候 不知道怎么回事 挡住了 滑不上去，于是我就看微信是怎么做的，微信的做法就是滑动的时候 让input 失去焦点
$("main").on("scroll",function(){
	$('input').blur()
})
于是就有了这段代码，在移动端的话  可以吧 scroll事件 换成 touchmove 比较友好。

基本就这了。。。不喜勿喷！！！

# 热点图

```html
<!DOCTYPE html>
<html>
	<head>
		<style>
			#test {
				width: 200px;
				height: 200px;
				background-color: black;
				opacity: 0.5;
			}
			@keyframes hotspot{
				0%{}
				70%{
					width: 40px;
					height: 40px;
					opacity: 1;
				}
				100%{
					width: 70px;
					height: 70px;
					opacity: 0;
				}
			}
			.hotspot{
				position: absolute;
				top: 100px;
				left: 100px;
			}
			.hotspot #dot{
				width: 8px;
				height: 8px;
				background-color: aqua;
				border-radius: 50%;
			}
			.hotspot [class^="wave"]{
				width: 8px;
				height: 8px;
				box-shadow: 0 0 12px aqua;
				
				position: absolute;
				top: 50%;
				left: 50%;
				transform: translate(-50%,-50%);
				border-radius: 50%;
				
				animation: hotspot 1.2s linear infinite;
			}
			.hotspot .wave2{
				animation-delay: 0.4s;
			}
			.hotspot .wave3{
				animation-delay: 0.8s;
			}
		</style>
	</head>
	<body>
		<div id="test">
			<div class="hotspot">
				<div id="dot"></div>
				<div class="wave1"></div>
				<div class="wave2"></div>
				<div class="wave3"></div>
			</div>
		</div>
	</body>
</html>
```

# 使用逐帧动画

```css
@keyframes play{
  0%{
    background-position: 0,0;
  }
  100%{
    background-position: -图片长度,0;
  }
}
.anima{
  width: 200px;
  height: 100px;
  background: url(图片位置) no-repeat;
  animation: play 2s steps(有几张图) infinite;
}
```


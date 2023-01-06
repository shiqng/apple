# 基于animejs封装的方法说明

## 方法说明（附调用案例）

### 可选参数总结

<!--

可选参数（字符串形式）或 回调形式

1. "duration = 5000" 	动画过度时长（毫秒为单位，默认值为500）
2. "delay=0"    动画是否延迟执行（毫秒为单位，默认值为0）
3. "easing=linear" 动画曲线（可以传入三次贝塞尔，默认值为linear） https://matthewlein.com/tools/ceaser  在这网站调事半功倍
4. “opacity=1” 透明值 （0dom元素透明，默认值为1）
5. 回调函数，动画执行完后执行

-->

```
案例
this.levelAnime('.level', 300, "duration = 500", "delay=0", "easing=linear","opacity=1", () => {
	console.log('动画结束了')
})
等价于
this.levelAnime('.level', 300, () => {
	console.log('动画结束了')
})
```



### levelAnime

<!--左右刷出来的动画 控制div的width  

   必要参数

1.   css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器 
2.  目标dom的width值 （px为单位）

-->

```vue
this.levelAnime('.level', 300, "duration = 5000", "delay=500", "easing=cubicBezier(.5, .05, .1, .3)","opacity=0.8", () => {
	console.log('动画结束了')
})
```



### verticalityAnime

<!--垂直刷出来的动画 控制div的 height

   必要参数

1.   css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器 
2.  目标dom的 height值 （px为单位）

-->

```
this.verticalityAnime('.verticality', 300)
```



### levelMoveAnime

<!--左右飘出来的动画，控制div即可 left

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.    目标dom的left值

  -->

```
this.levelMoveAnime('.piao3', 50);
```



### bottomMoveAnime

<!--上下飘出来的动画，控制div的bottom值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的bottom值

  -->

```
this.bottomMoveAnime('.piao3', 50);
```



### rightMoveAnime

<!--左右飘出来的动画，控制div的right值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的right值

  -->

```
this.rightMoveAnime('.piao3', 50);
```



### whAnime

<!--刷出来的动画，控制div的宽高值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的width值
3. 目标dom的height值

  -->

```
this.rightMoveAnime('.piao3', 500,200);
```



### verticalityMoveAnime

<!--飘出来的动画，控制div的top值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的top值

  -->

```
this.verticalityMoveAnime('.piao3', 500);
```



### opacityAnime

<!--淡入淡出的动画，控制div的opacity值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的opacity值

  -->

```
this.opacityAnime('.piao3', 1);
```



### scaleAnime

<!--放大缩小的动画，控制div的scale值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的scale值

  -->

```
this.scaleAnime('.piao3', 2);
```



### reversalAnime

<!--翻转的动画，控制div的rotateY 值

   必要参数

1. ​    css选择器  可以以数组形式 如['.id1','.id2','.id3'] 或单个选择器
2.   目标dom的rotateY 值

 无可选参数，因为  transition优先级高于 animejs

-->

```
this.reversalAnime('.r1', 0);
```



# 基于svg实现的动画（路径动画）

### 线动画

```html
<div class="svg_icon1">
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="338px"
         height="866px">
        <path fill-rule="evenodd" stroke="rgb(94, 152, 129)" stroke-width="6px" stroke-dasharray="24, 12"
              stroke-linecap="butt" stroke-linejoin="miter" fill="none"
              d="M29.001,6.000 L305.999,6.000 C318.703,6.000 328.999,16.297 328.999,29.000 L328.999,834.000 C328.999,846.703 318.703,857.000 305.999,857.000 L29.001,857.000 C16.297,857.000 6.000,846.703 6.000,834.000 L6.000,29.000 C6.000,16.297 16.297,6.000 29.001,6.000 Z" />
    </svg>
</div>
```

```less
.svg_icon1 {

    // svg {
    //     transform: scale(0.5);
    //     .positionLT(2645/2-329/4px, 748/2-857/4px);
    // }
    path {
        animation: test2 8s linear infinite;
    }

    @keyframes test2 {
        from {
            stroke-dashoffset: 2400;
        }

        to {
            stroke-dashoffset: 1200;
        }
    }
}
```



### 路径动画

```html
// 将svg路径 赋值给 --path
<div class="click page7_icon1 cycle" style='--path:"M45.172,44.735 L926.204,44.735 L1139.500,330.500 "'>
```

```css
.cycle {
    width: 25px;
    height: 25px;
    background: white;
    border-radius: 50%;
    offset-distance: 0%;
    offset-path: path(var(--path));
    animation: move 3s infinite ease-in-out;
    @keyframes move {
        0% {
            offset-distance: 0%;
        }

        100% {
            offset-distance: 100%;
        }
    }
}
```

### 纯css箭头组动画

```html
<div class="iconGroup">
    <div class="arrow-right">
    </div>
    <div class="arrow-right">
    </div>
    <div class="arrow-right">
    </div>
    <div class="arrow-right">
    </div>
    <div class="arrow-right">
    </div>
</div>
```

```less
.iconGroup {
    .arrow-right {
        opacity: 0;
        height: 120px;
        width: 60px;
        display: inline-block;
        position: relative;

        &::after {
            content: "";
            height: 60px;
            width: 60px;
            top: 12px;
            border-width: 25px 25px 0 0; // 箭头大小
            border-color: greenyellow;
            border-style: solid;
            transform: matrix(0.71, 0.71, -0.71, 0.71, 0, 0);
            position: absolute;
        }

        &:nth-child(5) {
            animation: iconAnime 2s linear 2000ms infinite alternate;
        }

        &:nth-child(4) {
            animation: iconAnime 2s linear 1500ms infinite alternate;
        }

        &:nth-child(3) {
            animation: iconAnime 2s linear 1000ms infinite alternate;
        }

        &:nth-child(2) {
            animation: iconAnime 2s linear 500ms infinite alternate;
        }

        &:nth-child(1) {
            animation: iconAnime 2s linear 0ms infinite alternate;
        }
    }

    @keyframes iconAnime {
        100% {
            opacity: 0.08;
        }

        0% {
            opacity: 1;
        }
    }
}
```



### 矩形生长动画

```html
// 背景图 使用requestAnimeFrame动态改变图片的高度
<div class="rect1"></div>
```

```javascript
// 挂载到vue 原型
/*参数说明
*dom 标签
*height 目标高度
*dateNow 当前时间戳 Date.now()
*time 完成时间（在多少毫秒内完成这个动画）
*/
Vue.prototype.raf1 = function (dom, height, dateNow, time) {
  let nowH = parseInt(getComputedStyle(dom).height)
  if (nowH >= height) {
    this.textFlag = true
    return true
  } else {
    requestAnimationFrame((beginTime) => {
      beginTime = Date.now() - dateNow
      if (beginTime <= time) {
        let h = parseInt(height * (beginTime / time))
        dom.style.height = (h) + 'px'
      } else {
        dom.style.height = height + 'px'
      }
      this.raf1(dom, height, dateNow, time)
    })
  }

}
```

```vue
//调用
this.r1 = document.querySelector('.rect1')
this.raf1(this.r1, 300, Date.now(), 1000)
```



```css
.rect1 {
    width: 473px;
    height: 0px;
    position: absolute;
    left: 0px;
    bottom: 2160-1161-770px;
    background: url("../assets/images/page14rect1.png") center center / 100% 100% no-repeat;
}
```



# 华为展厅常用css实现的动画

### 点击后，放大高亮呼吸

```css
//动态为图片div加上 active 类
.active {
    transform: scale(1.51);
    filter: brightness(170%) drop-shadow(0px 0px 30px rgb(124, 163, 232));
    animation: lightBreathe 1s linear infinite alternate;
    
    @keyframes lightBreathe {
        0% {
            opacity: 0.65;
        }

        100% {
            opacity: 1;
        }
    }
}
```



### 三层呼吸

```html
// 只需要给多一个 定位的类（绝对定位）
<div class="breathing"></div>
```

```scss

.breathing {
	width: 20px;
	height: 20px;
	background: rgb(178, 217, 135);
	border-radius: 50%;
	filter: grayscale(50%);
	transform: scale(2);
	position: absolute;
	overflow: visible;
	&::before {
		content: '';
		width: 30px;
		height: 30px;
		background-image: radial-gradient(transparent 40%, rgb(178, 217, 135) 100%);
		border-radius: 50%;
		animation: breathing_1_am 1.5s linear infinite alternate;
		position: absolute;
		left: -25%;
		top: -25%;
	}

	&::after {
		content: '';
		width: 30px;
		height: 30px;
		background-image: radial-gradient(transparent 40%, rgb(178, 217, 135) 100%);
		border-radius: 50%;
		animation: breathing_2_am 1.5s linear infinite alternate;
		-webkit-animation: breathing_2_am 1.5s linear infinite alternate;
		position: absolute;
		left: -25%;
		top: -25%;
	}

	@keyframes breathing_1_am {
		0% {
			transform: scale(1.15);
		}

		100% {
			transform: scale(1.7);
		}
	}

	@keyframes breathing_2_am {
		0% {
			transform: scale(.5);
		}

		100% {
			transform: scale(1.05);
		}
	}


}
```



### 小手+呼吸

```
// 只需要给多一个 定位的类（绝对定位）
<div class="finger click">
    <img src="../assets/images/finger2.png" alt="" srcset="">
    <div class="breathing"></div>
</div>
```

```css
.finger {
    position: relative;
    img {
        position: absolute;
        left: 29px;
        top: 9px;
        width: 55px;
        height: 84px;
        animation: fingerAnime 1.5s infinite alternate;
    }

    .breathing {
        width: 20px;
        height: 20px;
        background: rgb(178, 217, 135);
        border-radius: 50%;
        filter: grayscale(50%);
        transform: scale(2);
        position: absolute;
		overflow: visible;
        &::before {
            content: '';
            width: 30px;
            height: 30px;
            background-image: radial-gradient(transparent 40%, rgb(178, 217, 135) 100%);
            border-radius: 50%;
            animation: breathing_1_am 1.5s linear infinite alternate;
            position: absolute;
            left: -25%;
            top: -25%;
        }

        &::after {
            content: '';
            width: 30px;
            height: 30px;
            background-image: radial-gradient(transparent 40%, rgb(178, 217, 135) 100%);
            border-radius: 50%;
            animation: breathing_2_am 1.5s linear infinite alternate;
            -webkit-animation: breathing_2_am 1.5s linear infinite alternate;
            position: absolute;
            left: -25%;
            top: -25%;
        }

        @keyframes breathing_1_am {
            0% {
                transform: scale(1.15);
            }

            100% {
                transform: scale(1.7);
            }
        }

        @keyframes breathing_2_am {
            0% {
                transform: scale(.5);
            }

            100% {
                transform: scale(1.05);
            }
        }
	}
}
```



### 锥形渐变

```html
//--percent1 自定义变量，一段区域一种颜色 --max:360 最大值（结束值）
<div id='circle' class="circle" style="--percent1:0;--percent2:0;--percent3:0;--percent4:0;--max:360"></div>
```

```vue
/*
*obj.startTime = 0
*obj.beginVal = 0 // 开始值
*obj.endVal = 360 // 结束值
*obj.step = 1 // 跨度
*obj.time = 16 // 每多少毫秒执行
*obj.name = '--percent1' // 值
/
raf(obj) {
    if (obj.beginVal >= obj.endVal) {
    	return
    }
requestAnimationFrame((beginTime) => {
	//beginTime 任务执行时间 毫秒
	if (beginTime - obj.startTime > obj.time) {
		obj.beginVal += obj.step
		this.dom.style.setProperty(obj.name, `${obj.beginVal}deg`)
		this.dom.style.setProperty('--value', obj.beginVal)
		obj.startTime = beginTime
	}
	if (obj.beginVal < 90) {
        obj.time = 16
        this.raf(obj)
    } else if (obj.beginVal >= 90 && obj.beginVal < 180) {
        obj.time = 50
        obj.name = '--percent2'
        this.raf(obj)
    } else if (obj.beginVal >= 180 && obj.beginVal < 270) {                                                                             obj.time = 60                                                                                                                   obj.name = '--percent3'                                                                                                         this.raf(obj)
    } else if (obj.beginVal >= 270 && obj.beginVal < 360) {
        obj.time = 16
        obj.name = '--percent4'
        this.raf(obj)
    }
  })
}
```



```css
.circle {
    width: 300px;
    height: 300px;
    background: #fff;
    border-radius: 50%;
    background: conic-gradient(red 0,
            red var(--percent1),
            blue var(--percent1),
            blue var(--percent2),
            green var(--percent2),
            green var(--percent3),
            black var(--percent3),
            black var(--percent4),
            black var(--percent4)); //这里控制一开始圆环的颜色
    position: relative;
    counter-reset: percent var(--value);
}
.circle:before,
.circle:after {
    position: absolute;
    content: '';
    margin: auto;
    left: 0px;
    right: 0px;
    bottom: 0px;
    top: 0px;
    border-radius: 50%;
    width: 90%; //圆环大小配置
    height: 90%; //圆环大小配置
    background: black; //内圈颜色
}

.circle:after {
    content: counter(percent);
    text-align: center;
    line-height: 12px;
    font-size: 30px;
    height: 12px;
    color: #fff; //数字颜色
}

```





### 矩形流光

```html
<div class="click text1"></div>
```

```less
.text1 {
    width: 456px;
    height: 154px;
    opacity: 1;
    background: url("../assets/images/btn1.png") center center / 100% 100% no-repeat;
    // border-radius: 10px;
    transition: all .3s;
    cursor: pointer;
    position: relative;

    &::before,
    &::after {
        content: "";
        position: absolute;
        width: 100%;
        height: 100%;
        border: 3px solid rgba(124, 211, 255, .7);
        transition: all .5s;
        animation: clippath 3s infinite linear;
        border-radius: 26px;
    }

    &::after {
        animation: clippath 3s infinite 1.5s linear;
    }

    @keyframes clippath {

        0%,
        100% {
            clip-path: inset(0 0 90% 0);
        }

        25% {
            clip-path: inset(0 90% 0 0);
        }

        50% {
            clip-path: inset(90% 0 0 0);
        }

        75% {
            clip-path: inset(0 0 0 90%);
        }
    }
}
```



### 内发光

```html
// 加上这个类 boxAnime 即可
<div class="click btn1 boxAnime"></div>
```

```css
.boxAnime {
    animation: boxShadowInset 3s linear infinite alternate;
}

@keyframes boxShadowInset {
    0% {
        box-shadow: 0px 0px 25px rgb(64, 248, 255) inset;
    }

    50% {
        box-shadow: 0px 0px 45px rgb(64, 248, 255) inset;
    }

    100% {
        box-shadow: 0px 0px 25px rgb(64, 248, 255) inset;
    }
}
```



### 图片扫光

```html
<div class="click btn2 "></div>
```

```less
.btn2 {
    width: 456px;
    height: 154px;
    opacity: 1;
    background: url("../assets/images/btn1.png") center center / 100% 100% no-repeat;
    transition: all.5s;
    position: relative;

    &::after {
        content: '';
        width: 5%;
        height: 100%;
        position: absolute;
        background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
        box-shadow: 30px;
        overflow: hidden;
        transform: skew(-26deg, 0deg);
        animation: move 2s linear infinite;
    }

    @keyframes move {
        0% {
            left: 0%;
            opacity: 0;
        }

        50% {
            left: 43%;
            opacity: 1;
        }

        100% {
            left: 86%;
            opacity: 0;
        }
    }
}
```

# 文字特效

### 文字扫光

```html
//data-text 文本内容 title类是必要的样式可自定义
<div data-text="Bring Ultimate User Experience for Qatar World Cup" class="title t1"></div>
<div data-text="体维优协同打造卡塔尔世界杯精品网" class="title t2"></div>
```

```css
.title {
    // font-family: "Huawei Sans";
    background-color: rgb(255, 192, 0);
    color: transparent;
    background-clip: text;
    -webkit-background-clip: text;
}

.title::after {
    content: attr(data-text);
    -webkit-animation: shine 5s infinite linear;
    animation: shine 5s infinite linear;
    background-image: linear-gradient(120deg, transparent 0%, transparent 6rem, #0ef3be 11rem, transparent 11.15rem); //扫光颜色
    background-clip: text;
    -webkit-background-clip: text;
    background-size: 150% 100%;
    @keyframes shine {
        0% {
            background-position: 50% 0;
        }

        100% {
            background-position: -190% 0;
        }
	}
}

```

### 文字阴影

```html
 // data-text为阴影内容
<div class="shadow" data-text="showName">showName</div>
```

```less
.shadow {
    color: rgb(112, 133, 112);
    font-size: 120px;

    &::before {
        content: attr(data-text);
        position: absolute;
        color: black;
        transform: translate(-8px, 7px) scaleY(0.5) skew(32deg);
        z-index: -1;
        filter: blur(1.5px);
        -webkit-mask-image: linear-gradient(transparent, #000);
    }
}
```



### text-showad(凸出的感觉)

```html
<div class="word">3Dword</div>
```

```css
.word {
    font-size: 120px;
    color: goldenrod;
    text-shadow: 0.1px 0.1px rgba(50, 118, 181, 0.8), 0.2px 0.2px rgba(50, 118, 181, 0.8), 0.3px 0.3px rgba(50, 118, 181, 0.8), 		0.4px 0.4px rgba(50, 118, 181, 0.8), 0.5px 0.5px rgba(50, 118, 181, 0.8), 0.6px 0.6px rgba(50, 118, 181, 0.8),
        0.7px 0.7px rgba(50, 118, 181, 0.8), 0.8px 0.8px rgba(50, 118, 181, 0.8), 0.9px 0.9px rgba(50, 118, 181, 0.8), 1px 1px 			rgba(50, 118, 181, 0.8), 1.1px 1.1px rgba(50, 118, 181, 0.8), 1.2px 1.2px rgba(50, 118, 181, 0.8), 1.3px 1.3px rgba(50, 		118, 181, 0.8);
}
```



### text-showad(立体的感觉)

```html
<div class="a">Aword</div>
```

```css
.a {
    font-size: 120px;
    color: goldenrod;
    text-shadow: 0px 0.1px rgba(50, 118, 181, 0.8), 0px 0.2px rgba(50, 118, 181, 0.8), 0px 0.3px rgba(50, 118, 181, 0.8), 0px 0.4px rgba(50, 118, 181, 0.8), 0px 0.5px rgba(50, 118, 181, 0.8), 0px 0.6px rgba(50, 118, 181, 0.8),
        0px 0.7px rgba(50, 118, 181, 0.8), 0px 0.8px rgba(50, 118, 181, 0.8), 0px 0.9px rgba(50, 118, 181, 0.8), 0px 1px rgba(50, 118, 181, 0.8), 0px 1.1px rgba(50, 118, 181, 0.8), 0px 1.2px rgba(50, 118, 181, 0.8), 0px 1.3px rgba(50, 118, 181, 0.8),
        0px 1.4px rgba(50, 118, 181, 0.8), 0px 1.5px rgba(50, 118, 181, 0.8), 0px 1.6px rgba(50, 118, 181, 0.8), 0px 1.7px rgba(50, 118, 181, 0.8), 0px 1.8px rgba(50, 118, 181, 0.8), 0px 1.9px rgba(50, 118, 181, 0.8), 0px 2px rgba(50, 118, 181, 0.8);
}
```



### 背景线性渐变，文字之外剪掉，文字透明

```html
<div class="content">
            文字颜色渐变
        </div>
```

```css
.content {
    font-size: 120px;
    background: -webkit-linear-gradient(right, #FF0000, #00FF00, black);
    /*设置线性渐变*/
    /*为了支持更多的浏览器*/
    -webkit-background-clip: text; //文字之外的区域都将被裁剪掉
    /*背景被裁剪到文字*/
    -webkit-text-fill-color: transparent; //把文字变透明
    /*设置文字的填充颜色*/
}
```



### text-stroke(新特性，只支持谷歌内核)

```html
<div class="wordBorder">wordBorder</div>
```

```css
.wordBorder {
    font-size: 120px;
    -webkit-text-stroke: 5px #2173FF;
}
```



### 线性渐变同上，改变background-position

```html
<div class="bg">
    <p class="shine">无人做你的光芒就自己照亮前方
    </p>
</div>
```

```less
.bg {
    background: #000;
    /*设置元素背景颜色*/
    width: 1000px;
    /*设置元素宽度*/
    height: 200px;
    margin: 0 auto;
    position: relative;

    /*设置元素高度*/
    .shine {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 1000px;
        font-size: 60px;
        text-align: center;
        background: -webkit-linear-gradient(left, #0f0, #00f) 0 0 no-repeat;
        /*设置线性渐变*/
        -webkit-background-size: 160px;
        /*设置背景大小*/
        -webkit-background-clip: text;
        /*背景被裁剪到文字*/
        -webkit-text-fill-color: rgba(255, 255, 255, 0.3);
        /*设置文字的填充颜色*/
        -webkit-animation: shine1 3s infinite;

        /*设置动画*/
        @keyframes shine1 {

            /*创建动画*/
            0% {
                background-position: 0 0;
            }

            100% {
                background-position: 100% 100%;
            }
        }
    }
}
```


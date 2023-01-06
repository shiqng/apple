<script src="https://www.kkkk1000.com/js/pixi4.8.2.js"></script>

# App.vue

```
<template>
        <!-- pixi-->
      <!-- <div class="pixi"></div> -->
      <!-- canvas-->
      <ImgAnimation :time="1000" :imgList="alienImages" :pause="pause" @imgPuase="pause = !pause"/>
</template>

<script>
import ImgAnimation from './views/imgAnimation.vue'
export default {
  data() {
    return {
      pause:false,
      alienImages:[ 
        require('./assets/images/gif/1.png'),require('./assets/images/gif/2.png'),require('./assets/images/gif/3.png'),
        require('./assets/images/gif/4.png'),require('./assets/images/gif/5.png'),require('./assets/images/gif/6.png'),
        require('./assets/images/gif/7.png'),require('./assets/images/gif/8.png'),require('./assets/images/gif/9.png'),
        require('./assets/images/gif/10.png'),require('./assets/images/gif/11.png'),require('./assets/images/gif/12.png'),
        require('./assets/images/gif/13.png'),require('./assets/images/gif/14.png'),require('./assets/images/gif/15.png'),
        require('./assets/images/gif/16.png'),require('./assets/images/gif/17.png'),require('./assets/images/gif/18.png'),
        require('./assets/images/gif/19.png'),require('./assets/images/gif/20.png'),require('./assets/images/gif/21.png'),
        require('./assets/images/gif/22.png'),require('./assets/images/gif/23.png'),require('./assets/images/gif/24.png'),
        require('./assets/images/gif/25.png'),require('./assets/images/gif/26.png'),require('./assets/images/gif/27.png'),
        require('./assets/images/gif/28.png'),require('./assets/images/gif/29.png'),require('./assets/images/gif/30.png')
        ]
    };
  },
  components:{
    ImgAnimation
  },
  mounted(){
  //pixi
    // this.test()
  },
  methods: {
    test(){
          let renderer = PIXI.autoDetectRenderer(700,600,{
              antialias: true,
              transparent: true,
              resolution: 1
          });
          let pixie;
          document.getElementsByClassName('pixi')[0].appendChild(renderer.view);
          let stage = new PIXI.Container();

          let alienImages = [require("./assets/images/gif/1.png"),require("./assets/images/gif/2.png"),require("./assets/images/gif/3.png"),require("./assets/images/gif/4.png"),require("./assets/images/gif/5.png"),require("./assets/images/gif/6.png"),require("./assets/images/gif/7.png"),require("./assets/images/gif/8.png"),require("./assets/images/gif/9.png"),require("./assets/images/gif/10.png"),require("./assets/images/gif/11.png"),require("./assets/images/gif/12.png"),require("./assets/images/gif/13.png"),require("./assets/images/gif/14.png"),require("./assets/images/gif/15.png"),require("./assets/images/gif/16.png"),require("./assets/images/gif/17.png"),require("./assets/images/gif/18.png"),require("./assets/images/gif/19.png"),require("./assets/images/gif/20.png"),require("./assets/images/gif/21.png"),require("./assets/images/gif/22.png"),require("./assets/images/gif/23.png"),require("./assets/images/gif/24.png"),require("./assets/images/gif/25.png"),require("./assets/images/gif/26.png"),require("./assets/images/gif/27.png"),require("./assets/images/gif/28.png"),require("./assets/images/gif/29.png"),require("./assets/images/gif/30.png")];
          let textureArray = [];
          new Promise(function(resolve,reject) {
              for (let i=0; i < 30; i++)
              {
                  let texture = PIXI.Texture.from(alienImages[i]);
                  textureArray.push(texture);
                  if (textureArray.length == 30 ) {
                      resolve();
                  }
              };
          }).then(function() {  
                  pixie = new PIXI.extras.AnimatedSprite(textureArray);
                  pixie.animationSpeed=0.3;
                  pixie.position.x = 0;
                  pixie.position.y = 0;
                  pixie.scale.x = 1;
                  pixie.scale.y = 1;
                  pixie.alpha = 1;
                  //把动画精灵添加到舞台
                  stage.addChild(pixie);
                  //播放动画精灵
                  pixie.play();
                  gameloop();
              }
          );
          
          function gameloop() {
                  if (pixie.currentFrame<30) {
                          renderer.render(stage);
                          requestAnimationFrame(gameloop);
                          // gameloop();
                  } else  {
                          pixie.gotoAndPlay(0);
                          gameloop();
                  }
          }
    },
  }
}
</script> 
<style lang="less">
*{
			margin:0;
			border:0;
			padding:0;
		}

.pixi{
  width: 700px;
  height: 600px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}
.pixi img{
  width: 100%;
}
</style>

```



# imgAnimation.vue

```
<template>
    <div class="vis-animation" ref="container">
        <!-- <img v-if="loaded" :src="src"> -->
        <img v-if="!loaded&&imgList.length>0" :src="imgList[0]">
        <canvas ref="canvasContainer" @click="imgPuase"></canvas>
    </div>
</template>

<script>
export default {
  name: 'vis-animation-canvas',
  props: {
    time: {
      type: Number,
      default: 1000
    },
    imgList: {
      type: Array,
      default: () => []
    },
    pause: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      loaded: false,
      progress: 0,
      src: '',
      index: 0,
      interval: 0,
      then: null,
      ctx: null,
      imgInstance: {},
      canvasInstance: {},
      width: 0,
      height: 0
    }
  },
  computed: {
    f1() {
        return this.$store.state.aaa
  }
    },
  mounted () {
    this.$nextTick(function () {
         this.width = 1176
    this.height = 2400
      this.canvas = this.$refs.canvasContainer
      this.ctx = this.canvas.getContext('2d')
      this.canvas.width = this.width
      this.canvas.height = this.height
      if (this.imgList && this.imgList.length > 0) {
        this.loadImage()
      }
    })
  },
  watch: {
    imgList (v) {
      if (v && v.length > 0) {
        this.loadImage()
      }
    },
    pause (n, o) {
      if (o && !n && this.imgList.length > 0) {
        this.play()
      }
    },
    f1(curVal, oldVal) {
        //初始化
        if(curVal === 0){
            this.index = 0
            this.interval= 0
            this.then= null
            // this.loaded = false
            this.src = ''
            this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
            this.ctx.drawImage(this.imgInstance[this.imgList[0]],
            0,
            0,
            this.canvas.width,
            this.canvas.height)
        }
    }
  },
  methods: {
    imgPuase(){
      this.$emit('imgPuase')
    },
    loadImage () {
      this.imgList.forEach((v,index) => {
          
        this.preLoadImg(v,index)
      })
    },
    preLoadImg (src,index) {
      let image = new Image()
      this.imgInstance[src] = image
      image.onload = () => {
        let canvas = document.createElement('canvas')
        let ctx = canvas.getContext('2d')
        canvas.width = this.width
        canvas.height = this.height
        ctx.drawImage(this.imgInstance[src],
          0,
          0,
          this.canvas.width,
          this.canvas.height)
        this.canvasInstance[src] = canvas
        this.progress++
        this.play()
        if(index === this.imgList.length - 1){
            this.$emit('changeMsg')
        }
      }
      image.onerror = () => {
        this.progress++
        this.play()
      }
      image.src = src
    },
    play () {
      if (!this.pause) {
        if (this.progress === this.imgList.length) {
          this.interval = this.time / this.imgList.length
          this.then = Date.now()
          this.animate()
        }
      } else {
        this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
      }
    },
    animate () {
      if (!this.pause) {
        requestAnimationFrame(() => {
          this.animate()
        })
      }
      let now = Date.now()
      let delta = now - this.then
      if (delta > this.interval) {
        this.loaded = true
        this.then = now - (delta % this.interval)
        this.src = this.imgList[this.index % (this.imgList.length)]
        this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
        this.ctx.drawImage(
          this.canvasInstance[this.src],
          0,
          0
        )
        this.index = (this.index + 1) % this.imgList.length
      }
      if (this.pause && this.index === 0) {
        this.loaded = true
        this.src = this.imgList[this.index]
      }
    }
  }
}
</script>
<style scoped lang="less">
    .vis-animation img{
        width: 948px;
        height: 1935px;
    }
        
    .vis-animation{
        width: 948px;
        height: 1935px;
    }
    canvas{
        position: absolute;
        top: 0;
        left: 0;
        z-index: 999;
        width: 948px;
        height: 1935px;
    }
        
</style>
```


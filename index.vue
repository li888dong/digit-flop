<template>
  <div
    class="num-container"
    :style="{
      'width': width+'px',
      'height':height+'px',
      'font-size': fontsize+'px',
      'color':fontcolor
    }">
    <span v-if="!numType && this.num!=0">{{ showNum }}</span>
    <span v-else>{{ num }}</span>
    <span v-if="!numType" ref="numbg" class="num-bg" :style="{backgroundColor:numbg}" :class="animate?'page-running'+num:''">{{ showNum }}</span>
  </div>
</template>

<script>
export default {
  name: "singleNum",
  props: {
    num: {
      type: String,
      required: true
    },
    duration: {
      type: Number,
      default: 1000
    },
    fontsize: {
      type: Number,
      default: 42
    },
    width: {
      type: Number,
      default: 36
    },
    height: {
      type: Number,
      default: 52
    },
    fontcolor:{
      type:String,
      default:'#00e9e8'
    },
    numbg:{
      type:String,
      default:'#0c5e85'
    }
  },
  data() {
    return {
      timer: null,
      showNum: 0,
      showNumBg: 0,
      animate: true
    }
  },
  computed: {
    numType() {
      return isNaN(this.num / 1)
    }
  },
  watch: {
    num() {
      if (!this.numType) {
        this.playing()
      } else {
        this.showNum = this.num
        this.animate = false
      }
    }
  },
  mounted() {
    if (!this.numType) {
      this.playing()
    } else {
      this.showNum = this.num
      this.animate = false
    }

  },
  beforeDestroy() {
    clearInterval(this.timer)
  },
  methods: {
    playing() {
      if (this.num == 0 && this.num === null) {
        this.showNum = 0
        this.num = 0
        this.animate = false
      } else {
        this.timer = setInterval(() => {
          if (this.showNum === (this.num / 1)) { //当前滚动数字和传入的目标数字相等时停止动画 清除定时器
            this.animate = false
            clearInterval(this.timer)
            return
          } else {
            this.animate = true//动画开始运动
            this.showNum++ //随动画数字加

            if (this.showNum === 10) { //0-9，满10归0
              this.showNum = 0
              this.animate = false
            }
          }
        }, (this.duration / this.num))//动画持续时间 有待优化
      }
    }
  }
}
</script>

<style scoped>
  .num-container{
    position: relative;
    perspective:150px;
    display: inline-block;
    margin: 0 1px;
    text-align: center;
    border: 1px solid rgba(9, 244, 243, 0.2);

  }
  .num-bg{
    position: absolute;
    z-index: 0;
    left: 0;
    top: 0px;
    right: 0;
    bottom: 50%;
    height: 50%;
    overflow: hidden;
    background: #0c5e85;
    opacity: 1;
    border: 1px solid rgba(9, 244, 243, 0.2);
    transition: transform ease 0.5s;
    transform-origin: bottom;
  }

  .page-running0{

  }
  .page-running1{
    animation: page 2s linear 1;
  }
  .page-running2{
    animation: page 1s linear 2;
  }
  .page-running3{
    animation: page 0.6s linear 3;
  }
  .page-running4{
    animation: page 0.5s linear 4;
  }
  .page-running5{
    animation: page 0.4s linear 5;
  }
  .page-running6{
    animation: page 0.3s linear 6;
  }
  .page-running7{
    animation: page 0.26s linear 7;
  }
  .page-running8{
    animation: page 0.25s linear 8;
  }
  .page-running9{
    animation: page 0.2s linear 9;
  }
  @keyframes page {
    0%{
      transform: rotateX(0deg);
    }
    100%{
      transform: rotateX(-180deg);
    }
  }
</style>

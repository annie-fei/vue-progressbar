<template>
	<div class="progress-wrapper" :style="wrapStyle">
        <div class="progress" :style="pBarStyle">
            <div class="left" :style="leftStyle">
                <div class="ball" :style="ballStyle"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ProgressBar',
  props: {
    leftBg: String,
    bgc: String,
    ballBgc: String,
    height: String,
    width: String,
    percent: {
      type: Number,
      default: 10
    }
  },
  data: function () {
    return {
      wrapStyle: {
        'width': this.width
      },
      pBarStyle: {
        'backgroundColor': this.bgc,
        'height': this.height
      },
      leftStyle: {
        'width': this.percent + '%',
        'background': this.leftBg,
        'height': this.height
      },
      ballStyle: {
        'backgroundColor': this.ballBgc,
        'height': this.height + '3%',
        'width': this.height,
        'borderRadius': parseInt(this.height) / 2 + 'px',
        'right': -parseInt(this.height) / 2 + 'px'
      }
    }
  },
  computed: {
    progressElement () {
      return this.$el.getElementsByClassName('progress')[0]
    }
  },
  watch: {
    percent (cur, old) {
      if (cur < 100) {
        this.leftStyle.width = cur + '%'
      } else {
        this.leftStyle.width = '100%'
        this.ballStyle.backgroundImage = 'url("../../assets/logo.png")'
      }
    }
  }
}
</script>

<style scoped>
    .progress-wrapper{
        /*width:100%;*/
        display: inline-block;
        text-align: center
    }
    .progress{
        width:100%;
        height:20px;
        background-color: #ccc;
        /* overflow: hidden; */
        cursor: pointer;
    }
    .left{
        height:100%;
        width: 30%;
        background-color: greenyellow;
        position: relative;
    }
    .ball{
        height:120%;
        width:20px;
        -webkit-border-radius:10px;
        -moz-border-radius:10px;
        border-radius:10px;
        background-color: red;
        position: absolute;
        bottom: 0;
        right: -10px;
        background: url("../../assets/avatar.jpg") no-repeat center;
        background-size: 100%
    }
</style>

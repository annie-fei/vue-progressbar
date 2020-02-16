<template>
	<div class="test">
    <span>{{ startValue }}</span>
        <progress-bar width="40%" height="20px" leftBg="greenyellow" bgc="#ccc" ballBgc="red" :percent="percent">
          <template  v-slot:left></template>
        </progress-bar>
        <span>{{endValue}}</span>
        <div>当前值：{{currentValue}}, 占百分比 = {{percent}}%</div>
    </div>
</template>

<script>
import ProgressBar from './ProgressBar.vue'
export default {
  name: '',
  data: function () {
    return {
      currentValue: 10,
      percent: 0,
      startValue: 0,
      endValue: 150
    }
  },
  computed: {
  },
  methods: {
  },
  components: {
    'progress-bar': ProgressBar
  },
  mounted () {
    this.percent = this.currentValue / this.endValue * 100
    this.timer = window.setInterval(() => {
      if (this.percent < 100) {
        this.currentValue++
      }
    }, 100)
  },
  watch: {
    currentValue (cur, old) {
      this.percent = cur / this.endValue * 100
    }
  }
}
</script>

<style scoped>
    .test > div,span{
        margin: 10px;
        vertical-align:middle;
    }
</style>

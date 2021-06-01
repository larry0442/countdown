<template>
  <div class="homepage">
    <canvas
      id="canvas"
      style="display:bolck;margin: 50px auto;"
    >
      <!-- 优雅降级 -->
      当前浏览器不支持canvas,请更换火狐浏览器或者Chrome浏览器重试
    </canvas>
  </div>
</template>

<script>
import digit from '../utils/digit';
export default {
  name: 'HomePage',
  data () {
    return {

    }
  },
  mounted () {
    this.init();
  },
  methods: {
    init () {
      console.log(digit);
      const canvas = document.getElementById('canvas');
      const context= canvas.getContext('2d');
      console.log(context);

    },
  }
}
</script>

<style lang="css" scoped>
.homepage {
  width: 100%;
  height: 100%;
  text-align: center;
  color: red;
}
</style>
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
      WIDTH: 1024,
      HEIGHT: 768,
      MARGIN_LEFT: 30,
      MARGIN_TOP: 60,
      RADIUS: 8, // 小球半径
      endDate: new Date(2021, 5, 3, 0, 26, 36),
      currentShowTimeSeconds: 0
    }
  },
  mounted () {
    this.init();
  },
  methods: {
    init () {
      /* 初始化 */
      const canvas = document.getElementById('canvas');
      const context = canvas.getContext('2d');

      // 设置 canvas 大小
      canvas.width = this.WIDTH;
      canvas.height = this.HEIGHT;

      setInterval(() => {
        // 时间
        this.currentShowTimeSeconds = this.getCurrentShowTimeSeconds();
        // 渲染
        this.render(context);
      }, 500);

      // 时间
      // this.currentShowTimeSeconds = this.getCurrentShowTimeSeconds();

      // // 渲染
      // this.render(context);
    },

    // 渲染函数
    render (context) {
      // 获取时间
      const hours = parseInt(this.currentShowTimeSeconds / 3600);
      const minutes = parseInt((this.currentShowTimeSeconds % 3600) / 60);
      const seconds = parseInt(this.currentShowTimeSeconds % 60);

      // 清除画布
      if (this.currentShowTimeSeconds != 0) { context.clearRect(0, 0, this.WIDTH, this.HEIGHT); }
      // 绘制时间
      this.renderDigit(this.MARGIN_LEFT + 0 * (this.RADIUS + 1), this.MARGIN_TOP, parseInt(hours / 10), context);
      this.renderDigit(this.MARGIN_LEFT + 15 * (this.RADIUS + 1), this.MARGIN_TOP, parseInt(hours % 10), context);
      this.renderDigit(this.MARGIN_LEFT + 30 * (this.RADIUS + 1), this.MARGIN_TOP, 10, context);
      this.renderDigit(this.MARGIN_LEFT + 39 * (this.RADIUS + 1), this.MARGIN_TOP, parseInt(minutes / 10), context);
      this.renderDigit(this.MARGIN_LEFT + 54 * (this.RADIUS + 1), this.MARGIN_TOP, parseInt(minutes % 10), context);
      this.renderDigit(this.MARGIN_LEFT + 69 * (this.RADIUS + 1), this.MARGIN_TOP, 10, context);
      this.renderDigit(this.MARGIN_LEFT + 78 * (this.RADIUS + 1), this.MARGIN_TOP, parseInt(seconds / 10), context);
      this.renderDigit(this.MARGIN_LEFT + 93 * (this.RADIUS + 1), this.MARGIN_TOP, parseInt(seconds % 10), context);
    },
    /**
     * 
     * @description 渲染数字的函数
     * @param {x} number 开始位置x
     * @param {y} number 开始位置y
     * @param {num} number 具体数字
     * @param {context} Object context canvas上下文
     **/
    renderDigit (x, y, num, context) {
      // 颜色
      context.fillStyle = "rgb(0,102, 153)";
      for (let i = 0; i < digit[num].length; i++) {
        for (let j = 0; j < digit[num][i].length; j++) {
          if (digit[num][i][j] == 1) {
            // 渲染小球
            context.beginPath();
            /* 设想： x为我们开始点，小球在一个方形盒子内部，半径为r,并且四周留出1个像素的空隙，盒子边长为2*(r + 1)
            * 小球圆心： x` = x + 2(r+1) + (r+1), 
            */
            const r = this.RADIUS;
            const _x = x + j * 2 * (r + 1) + (r + 1);
            const _y = y + i * 2 * (r + 1) + (r + 1);
            context.arc(_x, _y, r, 0, 2 * Math.PI, false);
            context.closePath();
            context.fill();
          }
        }

      }
    },
    // 时间处理函数
    getCurrentShowTimeSeconds () {
      const currentTime = new Date();
      let diff = this.endDate.getTime() - currentTime.getTime();
      let result = Math.round(diff / 1000);
      return result >= 0 ? result : 0;
    }
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
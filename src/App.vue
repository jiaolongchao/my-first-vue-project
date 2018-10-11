<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <canvas id='canvas' ref='mycanvas' width="1000" height="600"></canvas>  
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
export default {
  name: "App",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      title: "test"
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      let canvas = this.$refs.mycanvas;
      let ctx = canvas.getContext("2d");
      //在画布上画一个圆
      ctx.beginPath(); // 新建一条路径
      ctx.arc(500, 300, 100, 0, Math.PI * 2); // 定义圆的路径
      // ctx.stroke(); // 绘制 定义的路径
      ctx.fillStyle = "red"; //规定填充圆的颜色
      ctx.fill();
      // 画一个圆 需要 圆心位置 半径 和填充颜色

      //去创造一个类，这个类用来创造不同圆
      function Circle(x, y, r) {
        this.x = x;
        this.y = y;
        this.r = r;
        this.dx = Math.random() * 10 - 5;
        this.dy = Math.random() * 10 - 5;
        this.color = `rgb(${Math.floor(Math.random() * 250)},${Math.floor(
          Math.random() * 250
        )},203)`;
        ary.push(this);
      }
      Circle.prototype.render = function() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.r, 0, 2 * Math.PI);
        ctx.fillStyle = this.color;
        ctx.fill();
      };
      Circle.prototype.update = function() {
        this.x += this.dx;
        this.y += this.dy;
        this.r--;
        if (this.r <= 0) {
          let that = this;
          ary = ary.filter(item => {
            return item != that;
          });
          return false;
        }
        return true;
      };
      var ary = [];
      canvas.onmousemove = function(e) {
        new Circle(e.clientX, e.clientY, 30);
      };
      setInterval(function() {
        ctx.clearRect(0, 0, 1000, 600);
        ary.forEach(item => {
          item.update() && item.render();
        });
      }, 20);
    }
  }
};
</script>
<style>
</style>

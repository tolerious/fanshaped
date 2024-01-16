<template>
  <div id="app">
    <div class="pie-chart-container">
      <svg width="200" height="200" viewBox="0 0 32 32">
        <circle r="16" cx="16" cy="16" fill="red" v-if="showSection1" />
        <path v-if="showSection2" :d="section2Path" fill="blue"></path>
        <path v-if="showSection3" :d="section3Path" fill="green"></path>
        <path v-if="showSection4" :d="section4Path" fill="yellow"></path>
      </svg>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      // 控制显示哪些扇形的布尔值
      showSection1: true,
      showSection2: true,
      showSection3: true,
      showSection4: true,
    };
  },
  computed: {
    section1Path() {
      return this.describeArc(16, 16, 16, 0, 90);
    },
    section2Path() {
      return this.describeArc(16, 16, 16, 90, 200);
    },
    section3Path() {
      return this.describeArc(16, 16, 16, 200, 270);
    },
    section4Path() {
      return this.describeArc(16, 16, 16, 270, 360);
    },
  },
  methods: {
    describeArc(x, y, radius, startAngle, endAngle) {
      var start = this.polarToCartesian(x, y, radius, endAngle);
      var end = this.polarToCartesian(x, y, radius, startAngle);
      var largeArcFlag = endAngle - startAngle <= 180 ? '0' : '1';
      var d = [
        'M',
        x,
        y,
        'L',
        start.x,
        start.y,
        'A',
        radius,
        radius,
        0,
        largeArcFlag,
        0,
        end.x,
        end.y,
        'L',
        x,
        y,
      ].join(' ');
      return d;
    },
    polarToCartesian(centerX, centerY, radius, angleInDegrees) {
      var angleInRadians = ((angleInDegrees - 90) * Math.PI) / 180.0;
      return {
        x: centerX + radius * Math.cos(angleInRadians),
        y: centerY + radius * Math.sin(angleInRadians),
      };
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.pie-chart-container {
  margin: 0 auto;
  max-width: 200px;
}
</style>

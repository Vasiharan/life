<template>
  <div>
    <header>
      <h4 id="grid-ref">roll-over grid</h4>
      <h4>{{ msg }}</h4>
      <svg :height="height" :width="width">
        <rect
          v-for="item in girdData"
          :key="item.id"
          :class="item.class"
          :id="item.id"
          :width="item.width"
          :height="item.height"
          :x="item.x"
          :y="item.y"
          :fill="item.fill"
          :stroke="item.stroke"
        />
      </svg>
    </header>

    <section id="grid"></section>
  </div>
</template>

<script>
// import * as d3 from "d3";
export default {
  name: "GirdChart",
  data() {
    return {
      msg: "👋 from the Gird Component",
      height: 500,
      width: 500,
      square: 20,
      girdData: []
    };
  },
  created() {
    let cells = 0;
    for (var c = 0; c < this.squaresColumn; c++) {
      for (var r = 0; r < this.squaresRow; r++) {
        this.girdData.push({
          class: `square row-${r} col-${c}s`,
          id: `s-${cells++}`,
          width: this.square,
          height: this.square,
          x: 20 * c,
          y: 20 * r,
          fill: "#7AC143",
          stroke: "#FDBB30"
        });
      }
    }
  },
  methods: {},
  computed: {
    squaresRow() {
      return Math.round(this.width / this.square);
    },
    squaresColumn() {
      return Math.round(this.height / this.square);
    }
  }
};
</script>

<style>
.font-styles {
  font-family: "Source Code Pro", Consolas, monaco, monospace;
  font-size: 18px;
  line-height: 1.5;
  font-weight: 400;
}

body {
  position: relative;
  font-family: "Source Code Pro", Consolas, monaco, monospace;
  font-size: 18px;
  line-height: 1.5;
  font-weight: 400;
  color: #7ac143;
  background-color: #eee;
  padding: 20px;
}

h4 {
  font-size: 18px;
}
</style>
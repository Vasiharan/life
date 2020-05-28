<template>
  <div>
    <header>
      <h4>Alive count</h4>
      <h4>{{ totalAlive }}</h4>
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
          :fill="item.alive ? '#F5B041' : '#BFC9CA'"
          :stroke="item.stroke"
        />
      </svg>
    </header>
  </div>
</template>

<script>
// import * as d3 from "d3";
export default {
  name: "GirdChart",
  data() {
    return {
      msg: "👋 from the Gird Component",
      height: 200,
      width: 200,
      square: 20,
      cells: 0,
      girdData: [],
      initalGrid: [
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0],
        [0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0],
        [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0],
        [0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0],
        [0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 1, 0],
        [0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0],
        [0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
      ]
    };
  },
  created() {
    let row = 0;
    this.initalGrid.forEach(rows => {
      let col = 0;
      rows.forEach(cel => {
        console.log(`R:${row} c:${col}`, cel);
        this.createSquare(row, col, cel == 1);
        col++;
      });
      row++;
    });
  },
  mounted: function() {
    this.$nextTick(function() {
      window.setInterval(() => {
        this.girdData[
          parseInt(Math.floor(Math.random() * this.cells))
        ].alive = true;
      }, 1000);
    });
  },
  methods: {
    createSquare(row, col, alive) {
      this.girdData.push({
        class: `square row-${row} col-${col}s`,
        id: `s-${this.cells++}`,
        width: this.square,
        height: this.square,
        x: 20 * col,
        y: 20 * row,
        alive: alive,
        fill: alive ? "#F5B041" : "#BFC9CA",
        stroke: "#FDBB30"
      });
    }
  },
  computed: {
    squaresRow() {
      return Math.round(this.width / this.square);
    },
    squaresColumn() {
      return Math.round(this.height / this.square);
    },
    totalAlive() {
      return this.girdData.filter(x => x.alive).length;
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
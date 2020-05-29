<template>
  <span style="margin: 20px; display:inline-block;">
    <svg :height="height" :width="width">
      <rect
        v-for="(item) in this.girdData"
        v-bind:key="item.id"
        :class="item.class"
        :id="item.id"
        :width="square"
        :height="square"
        :x="item.x"
        :y="item.y"
        :fill="item.alive ? '#F5B041' : '#BFC9CA'"
        :stroke="item.stroke"
      />
    </svg>
  </span>
</template>

<script>
export default {
  name: "GirdChart",
  props: {
    girdConfig: Array
  },
  data() {
    return {
      msg: "👋 from the Gird Component",
      height: 0,
      width: 0,
      square: 20,
      cells: 0,
      rows: 0,
      cols: 0,
      girdData: [],
      initalGrid: this.girdConfig,
      mapGrid: {}
    };
  },
  created() {},
  mounted: function() {
    this.initialiseGrid();
    this.setGrid();
    this.setCycle();
  },
  methods: {
    initialiseGrid() {
      this.rows = this.initalGrid.length * 2;
      this.cols = this.initalGrid[0].length * 2;
      this.height = this.rows * this.square;
      this.width = this.cols * this.square;
    },
    setGrid() {
      for (let row = 0; row < this.rows; row++) {
        for (let col = 0; col < this.cols; col++) {
          this.createSquare(row, col, 0);
        }
      }
      let row = 0;
      this.initalGrid.forEach(rows => {
        let col = 0;
        rows.forEach(cel => {
          this.girdData.find(c => {
            return c.row == row && c.col == col;
          }).alive = cel == 1;
          col++;
        });
        row++;
      });
    },
    setCycle() {
      this.$nextTick(function() {
        window.setInterval(() => {
          this.evolve();
        }, 100);
      });
    },
    createSquare(row, col, alive) {
      this.girdData.push({
        class: `square row-${row} col-${col}s`,
        id: `${row}-${col}`,
        cell: this.cells++,
        row: row,
        col: col,
        x: 20 * col,
        y: 20 * row,
        alive: alive,
        fill: alive ? "#F5B041" : "#BFC9CA",
        stroke: "#FDBB30"
      });
    },
    getKeysOfNeighbours(row, col) {
      let keys = [];

      keys.push({ r: row - 1, c: col - 1 });
      keys.push({ r: row - 1, c: col });
      keys.push({ r: row - 1, c: col + 1 });

      keys.push({ r: row, c: col - 1 });
      keys.push({ r: row, c: col + 1 });

      keys.push({ r: row + 1, c: col - 1 });
      keys.push({ r: row + 1, c: col });
      keys.push({ r: row + 1, c: col + 1 });

      return keys.filter(key => {
        return (
          key.r >= 0 && key.c >= 0 && key.r < this.rows && key.c < this.cols
        );
      });
    },
    evolve() {
      let newGirdData = [];
      this.girdData.forEach(gird => {
        const keys = this.getKeysOfNeighbours(gird.row, gird.col);
        let alive = 0;
        keys.forEach(key => {
          if (
            this.girdData.find(c => {
              return c.row == key.r && c.col == key.c;
            }).alive
          ) {
            alive++;
          }
        });

        const cloneGirdData = Object.assign({}, gird);
        cloneGirdData.alive =
          (gird.alive && (alive === 2 || alive === 3)) ||
          (!gird.alive && alive === 3);
        newGirdData.push(cloneGirdData);
      });
      this.girdData = newGirdData;
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
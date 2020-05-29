
<template>
  <div id="app">
    <GridChart :girdConfig="girdOne" />
    <GridChart :girdConfig="girdTwo" />
    <GridChart :girdConfig="girdThree" />
    <GridChart :girdConfig="girdFour" />
    <GridChart :girdConfig="girdFive" />
    <GridChart :girdConfig="girdSix" />
    <GridChart :girdConfig="girdSeven" />
    <GridChart :girdConfig="girdEight" />
  </div>
</template>

<script>
import GridChart from "./components/Grid.vue";
import Grids from "./config/girds";

export default {
  name: "app",
  components: {
    GridChart
  },
  data: function() {
    return {
      loadData: [],
      girdOne: [],
      girdTwo: [],
      girdThree: [],
      girdFour: [],
      girdFive: [],
      girdSix: [],
      girdSeven: [],
      girdEight: []
    };
  },
  created() {
    this.girdOne = Grids.GLIDER;
    this.girdTwo = Grids.SMALL_EXPLODER;
    this.girdThree = Grids.EXPLODER;
    this.girdFour = Grids.ROW_OF_TEN;
    this.girdFive = Grids.LIGHTWEIGHT_SPACESHIP;
    this.girdSix = Grids.TUMBLER;
    this.girdSeven = Grids.CHECKBOARD;
    this.girdEight = Grids.BIG_SHAPE;
  },
  mounted() {},
  methods: {}
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
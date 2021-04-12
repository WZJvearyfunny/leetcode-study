<template>
  <div id="map"></div>
</template>

<script>
class Map {
  constructor(el, rect) {
    this.el = el;
    this.rows = Map.getStyle(el, "height") / rect;
    this.cells = Map.getStyle(el, "width") / rect;
  }
  static getStyle(el, attr) {
    return parseFloat(getComputedStyle(el)[attr]);
  }
}
{
  let map = document.querySelector("#map");
  let gameMap = new Map(map, 10);
  console.dir(gameMap);
}
export default {};
</script>

<style scoped>
#map {
  position: relative;
  width: 400px;
  height: 400px;
  background: #000;
}
</style>>
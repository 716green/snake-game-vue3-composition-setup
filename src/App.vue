<script setup>
import { ref, onMounted } from "vue";
import Player from "./components/Player.vue";

const rowCount = 35;
const columnCount = 19;

const columns = ref([]);
const rows = ref([]);

const buildGrid = async () => {
  const tempRows = [];
  for (let i = 0; i < rowCount; i++) {
    tempRows.push("");
  }
  rows.value = tempRows;

  const tempCols = [];
  for (let i = 0; i < columnCount; i++) {
    tempCols.push("");
  }
  columns.value = tempCols;
};

onMounted(async () => {
  await buildGrid();
});
</script>

<template>
  <section class="grid">
    <section style="position: absolute">
      <Player />
    </section>
    <div
      class="square-column"
      v-for="(_column, i) in columns"
      style=""
      :key="i"
    >
      <div
        class="square-row"
        style="width: 46px; height: 46px"
        v-for="(_row, j) in rows"
        :key="j"
      ></div>
    </div>
  </section>
</template>

<style lang="css">
.square-column {
  display: flex;
  background-color: white;
  margin: auto;
}
.square-row {
  display: flex;
  border: gray dashed 2px;
}
.grid {
  left: 0;
  top: 0;
  margin: auto;
  justify-content: center;
  height: calc(100vh - 45px);
  background-color: #000;
}
</style>

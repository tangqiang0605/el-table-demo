<template>
  <CustomTable :tableData="tableData"></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./CustomTable.vue";
const tableData = new Array(9).fill({
  a: "2016-05-03",
  b: "Tom",
  c: "No. 189, Grove St, Los Angeles",
  d: "No. 189, Grove St, Los Angeles",
  e: "2016-05-03",
  f: "Tom",
  g: "No. 189, Grove St, Los Angeles",
  h: "2016-05-03",
  i: "Tom",
});
</script>

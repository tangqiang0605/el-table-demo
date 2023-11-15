<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="a" label="aName" width="180" />
    <el-table-column prop="b" label="bName" width="180" />
    <el-table-column prop="c" label="cName" width="180" />
    <el-table-column prop="d" label="dName" width="180" />
    <el-table-column prop="e" label="eName" width="180" />
    <el-table-column prop="f" label="fName" width="180" />
    <el-table-column prop="g" label="gName" width="180" />
    <el-table-column prop="h" label="hName" width="180" />
    <el-table-column prop="i" label="iName" width="180" />
  </el-table>
</template>

<script lang="ts" setup>
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

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
defineProps<{
  tableData: Array<any>;
}>();
</script>

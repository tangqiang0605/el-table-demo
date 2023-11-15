<template>
  <CustomTable
    :tableData="tableData"
    :table-headers="tableHeaderMapper"
    v-loading="loading"
  ></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
import { getData } from "./api/index";
import { onMounted, ref } from "vue";
const tableData = ref<any>([]);
// 定义新的Header结构，key为column的prop/key，value为column的label
const tableHeaderMapper = {
  a: {
    label: "列a",
    width: "200",
  },
  b: "列b",
  c: "列c",
  d: "列d",
  e: "列e",
  f: "列f",
  g: "列g",
  h: "列h",
  i: "列i",
};
const loading = ref(false);
onMounted(() => {
  loading.value = true;
  getData().then((res: any) => {
    tableData.value = res.data;
    loading.value = false;
  });
});
</script>

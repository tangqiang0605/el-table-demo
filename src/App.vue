<template>
  <CustomTable :tableData="tableData"></CustomTable>
</template>

<script lang="ts" setup>
import CustomTable from "./components/custom-table/index.vue";
import { getData } from "./api/index";
import { onMounted, ref } from "vue";
const tableData = ref<any>([]);
onMounted(() => {
  getData().then((res: any) => {
    tableData.value = res.data;
  });
});
</script>

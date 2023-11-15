<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column
      v-for="(value, key) in tableHeaders"
      :key="key"
      :prop="key"
      :label="value"
    ></el-table-column>
  </el-table>
</template>

<script lang="ts" setup>
export type Mapper<T> = {
  [P in keyof T as string]?: string;
};
defineProps<{
  tableData: Array<any>;
  tableHeaders: Mapper<any>;
}>();
</script>

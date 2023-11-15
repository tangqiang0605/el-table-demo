<template>
  <el-table :data="tableData" style="width: 100%">
    <template v-for="slot in Object.keys($slots)" #[slot]>
      <slot :name="slot"></slot>
    </template>
  </el-table>
</template>

<script setup lang="ts">
defineProps<{
  tableData: Array<any>;
}>();
</script>

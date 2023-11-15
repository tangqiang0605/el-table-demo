<template>
  <el-table-column
    v-for="column in newTableHeader"
    v-bind="column"
  ></el-table-column>
</template>

<script lang="ts" setup>
import { ref, onMounted, onBeforeUpdate } from "vue";
export type Mapper<T> = {
  [P in keyof T as string]?: string | object;
};
const prop = defineProps<{
  tableHeaders: Mapper<any>;
}>();
const newTableHeader = ref<any>({});
const genNewTableHeader = () => {
  newTableHeader.value = { ...prop.tableHeaders };
  const rawAttr = prop.tableHeaders;
  for (let key in rawAttr) {
    let column = rawAttr[key];
    if (typeof column === "string") {
      Reflect.set(newTableHeader.value, key, {
        key: key,
        prop: key,
        label: column,
      });
    }

    // 其实此时一定是对象了，此处判断是用于ts类型收窄
    if (typeof column === "object") {
      // 设置默认的key
      if (!Reflect.has(column, "key")) {
        Reflect.set(column, "key", key);
      }
      if (!Reflect.has(column, "label")) {
        Reflect.set(column, "label", key);
      }
      // 设置默认的prop，如果该列是多选项，则不需要prop
      if (
        !Reflect.has(column, "prop") &&
        !(
          Reflect.has(column, "type") &&
          Reflect.get(column, "type") == "selection"
        )
      ) {
        Reflect.set(column, "prop", key);
      }
    }
  }
  console.log(newTableHeader.value);
};
onMounted(genNewTableHeader);
onBeforeUpdate(genNewTableHeader);
</script>

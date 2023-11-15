<template>
  <el-table-column v-for="column in newTableHeader" v-bind="column">
    <template v-for="(value, key) in column.slot" #[key]="scope">
      <slot :name="value" v-bind="scope">
        <div v-if="column.inner && String(key) == 'default'">
          <div
            v-if="typeof column.inner == 'string'"
            v-html="column.inner"
          ></div>
          <component v-else :is="column.inner"></component>
        </div>
      </slot>
    </template>
    <template v-if="!column.slot" #default>
      <div v-if="column.inner">
        <div v-if="typeof column.inner == 'string'" v-html="column.inner"></div>
        <component v-else :is="column.inner"></component>
      </div>
    </template>
  </el-table-column>
</template>

<script lang="ts" setup>
import { ref, onMounted, onBeforeUpdate, useSlots } from "vue";
export type Mapper<T> = {
  [P in keyof T as string]?: string | object;
};
const prop = defineProps<{
  tableHeaders: Mapper<any>;
}>();
const slots = useSlots();
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
      // 处理插槽
      const slotKeys = Object.keys(slots);
      for (let key of slotKeys) {
        const res = key.match(/^(\S+)-(\S+)/);
        // 查找不到则res为null
        if (res && res[2] == Reflect.get(column, "key")) {
          if (!Reflect.has(column, "slot")) {
            Reflect.set(column, "slot", {});
          }
          Reflect.set(Reflect.get(column, "slot"), res[1], res[0]);
        }
      }
    }
  }
  console.log(newTableHeader.value);
};
onMounted(genNewTableHeader);
onBeforeUpdate(genNewTableHeader);
</script>

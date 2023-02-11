<script setup lang="ts">
import { ref } from 'vue';
import NewColumnInput from '@/components/NewColumnInput.vue';
import NewTaskInput from '@/components/NewTaskInput.vue';
import ColumnList from '@/components/ColumnList.vue';
import type { IColumn } from '@/models/IColumn';
import type { ITask } from '@/models/ITask';


//state
const allColumns = ref<IColumn[]>([]);
const allTask = ref<ITask[]>([]);

// methods
const getColumn = (value: string) => {
  allColumns.value.push(value)
  console.log(allColumns.value)
};

const getTask = (value: string) => {
  allTask.value.push(value)
  console.log(allTask.value)
}

</script>

<template>
  <header class="header">
    <NewTaskInput placeholder="New task" @on-add-task="getTask"/>
    <NewColumnInput placeholder="New column" @on-add-column="getColumn"/>
  </header>
  <main >
    <ColumnList :columns="allColumns" :tasks="allTask"/>
  </main>
</template>

<style scoped lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  width: 600px;
  margin: 60px auto;
}
</style>
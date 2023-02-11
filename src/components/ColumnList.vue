<script setup lang="ts">
import Column from './Column.vue';
import type { IColumn } from '@/models/IColumn';
import type { ITask } from '@/models/ITask';

const props = defineProps<{
    columns: IColumn[],
    tasks: ITask[],
}>()
</script>

<template>
    <div class="column-list">
        <Column 
            v-for="column in columns" 
            :column="column"
            :tasks="tasks"
        />
    </div>
</template>

<style scoped lang="scss">
.column-list {
    width: 1000px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
</style>
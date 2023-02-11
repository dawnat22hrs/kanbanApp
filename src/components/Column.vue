<script setup lang="ts">
import Task from './Task.vue'
import type { IColumn } from '@/models/IColumn';
import type { ITask } from '@/models/ITask';


defineProps<{
    column: IColumn,
    tasks: ITask[],
}>()
</script>

<template>
    <div class="column">
        <div class="column__name">
            {{ column }}
        </div>
        <div class="column__block">
            <Task 
                v-for="task in tasks" 
                :task="task"
            />
        </div>
    </div>
    
</template>

<style scoped lang="scss">
    .column__name {
        width: fit-content;
        height: fit-content;
        background-color: #32a89d;
        border: 3px solid #277a73;
        font-size: 20px;
        display: flex;
        align-items: center;
        color: #fff;
        padding: 5px;
        cursor: pointer;
    }

    .column__block {
        width: fit-content;
        word-wrap: break-word;
        height: auto;
    }
</style>
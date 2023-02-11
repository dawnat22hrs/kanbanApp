<script setup lang="ts">
import type { ITask } from '@/models/ITask';

defineProps<{
    task: ITask,
}>()
</script>

<template>
    <div class="task">
        <label class="task__title">{{ task }}</label>
    </div>
</template>

<style scoped lang="scss">
.task {
    width: 300px;
    height: auto;
    display: flex;
    border: 1px solid #32a89d;
    border-radius: 10px;
    cursor: pointer;
    background-color: #fff;
    box-sizing: border-box;
    margin: 10px 0 10px 0;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.1);
    .task__title {
        display: flex;
        align-items: center;
        color: gray;
        background-color: #fff;
        cursor: pointer;
        margin: 10px;
    }
}
</style>
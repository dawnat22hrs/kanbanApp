<script setup>
defineProps({
    title: String
})

defineEmits(['onDeleteTask'])

</script>

<template>
    <div class="task">
        <label class="task__title">{{ title }}</label>
        <div class="task-del"
          @click="$emit('onDeleteTask')"
        >X</div>
    </div>
</template>

<style scoped lang="scss">
.task {
    width: 300px;
    height: auto;
    display: flex;
    align-items: center;
    border: 1px solid #32a89d;
    border-radius: 10px;
    cursor: pointer;
    background-color: #fff;
    box-sizing: border-box;
    margin: 10px 0 10px 0;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.1);
    position: relative;
    .task__title {
        color: gray;
        background-color: #fff;
        cursor: pointer;
        margin: 10px;
    }
}

.task-del{
  position: absolute;
  color: #32a89d;
  font-size: 18px;
  left: 92%;
  visibility: hidden;
  z-index: -1;
  opacity: 0;
}

.task:hover .task-del {
  visibility: visible;
  z-index: 99;
  opacity: 1;
}
</style>
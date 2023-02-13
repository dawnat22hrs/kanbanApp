<script setup>
import { ref } from 'vue';

const inputValueTask = ref('');

defineEmits(['onGetTask'])
</script>

<template>
    <div class="input__block">
        <input 
            type="text" 
            placeholder="New task" 
            class="input" 
            v-model="inputValueTask"
        >
        <button class="btn"
            @click="$emit('onGetTask', inputValueTask), inputValueTask=''"
        >+</button>
    </div>
</template>

<style lang="scss">
@import '@/assets/scss/fonts.scss';
.input {
    outline: none;
    border: none;
    background-color: transparent;
    border-bottom: 1px solid gray;
    font-size: 20px;
    font-family: 'Roboto';
}
.btn {
    width: 25px;
    height: 25px;
    border-radius: 30px;
    margin-left: 10px;
    font-size: 15px;
    font-weight: 400;
    border: none;
    cursor: pointer;
    background-color: #1E90FF;
    color: #fff;
}
</style>
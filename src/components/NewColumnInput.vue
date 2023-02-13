<script setup>
import { ref } from 'vue';

const inputValueColumn = ref('');

defineEmits(['onGetColumn']);
</script>

<template>
    <div class="input__block">
        <input 
            type="text" 
            placeholder="New column" 
            class="input" 
            v-model="inputValueColumn"
        >
        <button class="btn"
            @click="$emit('onGetColumn', inputValueColumn), inputValueColumn = ''"
        >+</button>
    </div>
</template>
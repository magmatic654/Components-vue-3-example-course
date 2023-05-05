<script setup>
import { ref } from 'vue';

const counter = ref(0)

const incremento = ()=> counter.value++


</script>

<template>
    <button @click="incremento">Contador: {{ counter }}</button>
</template>

<style>
</style>
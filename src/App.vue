<script setup>

import {ref, computed} from 'vue';

let counter = ref(0);
let arrayNumeros = ref([]);

const increment = () => {
    counter.value++;
};
const decrement = () => {
    counter.value--;
};
const reset = () => {
    counter.value=0;
};
const add = () => {
    arrayNumeros.value.push(counter.value);
};
const classCounter = computed( () => {
    if (counter.value === 0) return 'zero';
    return counter.value > 0 ? 'positivo' : 'negativo';
});
const blockNumber  = computed( () => {
    const number = arrayNumeros.value.find( (num) => num === counter.value);
    return number || number === 0;
});
</script>

<template>
    <div>
        <h2 v-bind:class="classCounter" >{{ counter }}</h2>
        <div class="btn-group" role="group" aria-label="Basic example">
            <button @click="increment" class="btn btn-primary">Click incremet</button>
            <button @click="decrement" class="btn btn-danger">Click decrement</button>
            <button @click="reset" class="btn btn-warning">Click reset</button>
            <button @click="add" :disabled="blockNumber" class="btn btn-success">Click add</button>
        </div>

        <ul class="list-group mt-4" >
            <li v-for="(numero,index) of arrayNumeros" :key="index" class="list-group-item">
                {{ numero }}
            </li>
        </ul>
    </div>
</template>

<style>
.positivo{
    color:green;
}
.negativo{
    color:red;
}
.zero{
    color:blue;
}
</style>
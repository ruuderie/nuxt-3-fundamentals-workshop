<script setup>
import { defineProps, ref, computed } from 'vue';

const props = defineProps({
  title: {
    type: String,
    default: 'Hello Frontend Masters!',
    required: true
  },
  endpoint: {
    type: String,
    default: 'todos',
    required: true
  },
  itemList: {
    type: Array,
    default: () => []
  }
});


const emit = defineEmits(['update:itemList']);

function fetchTodoList() {
  fetch(`https://jsonplaceholder.typicode.com/${props.endpoint}/`)
    .then(response => response.json())
    .then(json => {
        emit('update:itemList', json);
    });
}

</script>

<template>
    <!--Generic Template -->
<div class="section">
    <h1 class="title">{{ title }}</h1>
    <slot name="metrics"   />
    <button @click="fetchTodoList">Fetch Data</button>

    <slot name="hero" />

    <!--todo-->
    <ul>
    <slot name="items" :itemList="itemList" />
    </ul>
</div>
</template>

<style lang="scss">

</style>
<script>
import { defineNuxtComponent } from '#app';
export default defineNuxtComponent({
  name: 'App',
  data: () => ({
    message: 'Hello Nuxt.js',
    todoList: [],
    photosList:[]
  }),
  methods: {
    fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json())
        .then(json =>{
          this.todoList = json;
        });
    },
    fetchPhotos() {
      fetch('https://jsonplaceholder.typicode.com/photos')
        .then(response => response.json())
        .then(json =>{
          this.todoList = json;
        });
    },
  }
});
</script>

<template>
  <div>
    <img src="@/salym.eth_todo.png" alt=""/>
    <h1>Hello Frontend Masters!</h1>
    <button @click="fetchTodoList">Fetch Todo List</button>
   <!-- <pre> {{ todo }}</pre> -->
    <ul>
      <li v-for="item in todoList" :key="`todo-id-${item.id}`">
        <input type="checkbox" :checked="item.completed" /> 
        i{{ item.title }}
      </li>
    </ul>
    <ul>
      <li v-for="item in photosList" :key="`photo-id-${item.id}`">
        <img src={{item.url}} alt=""/>
      </li>
    </ul>
  </div>
</template>

<style>
img {
  width: auto;
  height: auto;
}
</style>

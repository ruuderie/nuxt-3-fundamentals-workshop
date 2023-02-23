<script>
import { defineNuxtComponent } from '#app';
export default defineNuxtComponent({
  name: 'App',
  data: () => ({
    message: 'Hello Nuxt.js',
    photosList:[]
  }),
  computed:{
    numberOfPhotos(){
      return this.photosList.length;
    },
    numberOfEvenPhotos(){
      return this.photosList.filter(item => item.id % 2 === 0).length;
    },
    numberOfOddPhotos(){
      return this.photosList.filter(item => item.id % 2 !== 0).length;
    }
  },
  methods: {
    fetchPhotos() {
      fetch('https://jsonplaceholder.typicode.com/photos')
        .then(response => response.json())
        .then(json =>{
          this.photosList = json;
        });
    },
  }
});
</script>

<template>
  <div>
    <img src="@/salym.eth_home.png" alt=""/>
    <h1>Photo Gallery!</h1>
    <p>Number of photos: {{numberOfPhotos}}</p>
    <p>Number of even photos: {{numberOfEvenPhotos}}</p>
    <p>Number of odd photos: {{numberOfOddPhotos}}</p>
    <button @click="fetchPhotos">Fetch Photo List</button>
    <ul>
      <li v-for="item in photosList" :key="`photo-id-${item.id}`">
        <img :src="item.thumbnailUrl" alt=""/>
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

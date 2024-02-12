<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import { reactive } from 'vue';

interface Post {
  id: number,
  userId: number,
  title: string,
  body: string
}

let posts = reactive(new Array<Post>())

function getData() {
  fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())
    .then(data => {
      console.log(`Posts: ${data}`);
      posts.push(...data)
    }) 
}

getData()

</script>

<template>
  <table>
    <thead>
      <tr>
        <td>User ID</td>
        <td>Id</td>
        <td>Title</td>
        <td>Body</td>
        <td>Total chars</td>
      </tr>
    </thead>
    <tbody>
      <tr v-for="post in posts"> 
        <template v-if="post.body.length < 150">
          <td>{{ post.id }}</td>
          <td>{{ post.userId }}</td>
          <td>{{ post.title }}</td>
          <td>{{ post.body }}</td>
          <td>{{ post.body.length }}</td>
        </template>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
  table {
    border: 2px solid black;
    max-width: 100%;
  }

  thead tr {
    background-color: rgb(226, 226, 226);
  }
</style>

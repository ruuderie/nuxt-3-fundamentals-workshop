<script setup>
import { ref, computed } from 'vue'

const todoList = ref([])

const route = useRoute()

const filteredTodoList = computed(() => {
  if (route.query.completed) {
    return completedItems.value
  } else {
    return remainingItems.value
  }
})

const completedItems = computed(() => {
  return todoList.value.filter(item => item.completed)
})

const remainingItems = computed(() => {
  return todoList.value.filter(item => !item.completed)
})
</script>

<template>
    

<Html>
    <Head>
        <Title>Todos</Title>
        <Link rel="preconnect" href="https://fonts.googleapis.com" />
<Link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<Link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Golos+Text&display=swap" />
       </Head>
</Html>

  <NuxtLayout name="todo">
  <div class="section">
    <NuxtPage v-if="route.params.id" />
    <BaseDisplay v-else title="Todo Viewer" v-model:itemList="todoList">
      <template v-slot:hero> </template>
      <template v-slot:metrics>
        {{ completedItems.length }} completed |
        {{ remainingItems.length }} remaining
      </template>
      <template v-slot:items>
        <li v-for="todo in filteredTodoList" :key="`todo-id-${todo.id}`">
          <input type="checkbox" :checked="todo.completed" />
          <NuxtLink :to="`/display/todos/${todo.id}`">{{
            todo.title
          }}</NuxtLink>
        </li>
      </template>
    </BaseDisplay>
  </div>
</NuxtLayout>
</template>

<style lang="scss"></style>

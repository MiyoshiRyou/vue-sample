<script setup lang="ts">
import { inject } from 'vue';
import { todoKey } from '../useTodo';

const state = inject(todoKey)
if (!state) {
  throw new Error('state is undefined')
}

const { todos, addTodo: _addTodo } = state

// const todos = inject('todos')
// const _addTodo = inject('addTodo')

const addTodo = (title: string) => {
  _addTodo(title)
}

</script>

<template>
  <div>
    <ul>
      <li :style="{ backgroundColor: 'aliceblue', marginBottom: '10px' }" v-for="todo in todos">{{ todo.title }}</li>
    </ul>
    <button @click="addTodo('add!')">Add</button>
  </div>
</template>

<style scoped>
</style>

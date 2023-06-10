<script setup lang="ts">
import { ref } from 'vue'

type Todo = {
  name: string
  isCompleted: boolean
}
const todos = ref<Todo[]>([])

const newTodoName = ref('')

const addTodo = () => {
  if (!newTodoName.value) return
  todos.value.push({ name: newTodoName.value, isCompleted: false })
}
</script>

<template>
  <div>Todoリスト</div>
  <ul>
    <li v-for="todo in todos.filter((v) => !v.isCompleted)" :key="todo.name">
      <div>{{ todo.name }}</div>
      <button @click="todo.isCompleted = true">完了</button>
    </li>
  </ul>
  <div>完了済みリスト</div>
  <ul>
    <li v-for="todo in todos.filter((v) => v.isCompleted)" :key="todo.name">
      <div>{{ todo.name }}</div>
      <button @click="todo.isCompleted = false">未完に戻す</button>
    </li>
  </ul>
  <div>
    <label>
      名前
      <input v-model="newTodoName" type="text" />
    </label>
    <button @click="addTodo">追加</button>
  </div>
</template>

<style></style>

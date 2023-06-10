<script setup lang="ts">
import { ref } from 'vue'

type Todo = {
  name: string
  isCompleted: boolean
}
const myStorage = localStorage
const todos = ref<Todo[]>(JSON.parse(myStorage.getItem('todolist') ?? '[]'))

const newTodoName = ref('')

const addTodo = () => {
  if (!newTodoName.value) return
  todos.value.push({ name: newTodoName.value, isCompleted: false })
  myStorage.setItem('todolist', JSON.stringify(todos.value))
}
</script>

<template>
  <div>Todoリスト</div>
  <ul>
    <li v-for="todo in todos.filter((v) => !v.isCompleted)" :key="todo.name">
      <div>{{ todo.name }}</div>
      <button
        @click="
          () => {
            todo.isCompleted = true
            myStorage.setItem('todolist', JSON.stringify(todos))
          }
        "
      >
        完了
      </button>
    </li>
  </ul>
  <div>完了済みリスト</div>
  <ul>
    <li v-for="todo in todos.filter((v) => v.isCompleted)" :key="todo.name">
      <div>{{ todo.name }}</div>
      <button
        @click="
          () => {
            todo.isCompleted = false
            myStorage.setItem('todolist', JSON.stringify(todos))
          }
        "
      >
        未完に戻す
      </button>
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

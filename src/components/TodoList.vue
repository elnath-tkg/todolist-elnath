<script setup lang="ts">
import { computed, ref } from 'vue'

interface Todo {
    task: string
    done: boolean
}

const todoList = ref<Todo[]>([
    {task: 'なろう講習会', done: false}
])


const doingTasks = computed(() => {
    return todoList.value.filter((todo) => todo.done == false)
})
const doneTasks = computed(() => {
    return todoList.value.filter((todo) => todo.done == true)
})

const newTask = ref('')

const addTask = () => {
  if(newTask.value != ''){
    todoList.value.push({ task: newTask.value, done:false})
    newTask.value = ''
  }
}

const finishTask = (endedTask: Todo) => {
  endedTask.done = true
}

</script>

<template>
  <div>
    <h1>TodoList</h1>
    <div>未完了のタスク</div>
    <ul>
      <li v-for="todo in doingTasks" :key="todo.task">
        <div>{{ todo.task }}</div>
        <button @click="finishTask(todo)">タスク完了！</button>
      </li>
    </ul>
    <div>完了したタスク</div>
    <ul>
      <li v-for="todo in doneTasks" :key="todo.task">
        <div>{{ todo.task }}</div>
      </li>
    </ul>
    <div>タスクの追加</div>
    <div>
      <label>
        タスク名
        <input v-model="newTask" type="text" />
      </label>
      <button @click="addTask">追加</button>
    </div>
  </div>
</template>

<style>
</style>
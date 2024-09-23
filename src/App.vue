<script setup lang="ts">
import { ref } from 'vue'
import Button from './components/button/Button.vue'

type Todos = {
  id: number
  text: string
  done: boolean
}[]

let id = 0
const text = ref('')
const todos = ref<Todos>([])

const addTodo = () => {
  const newTodo = {
    id: id++,
    text: text.value,
    done: false
  }
  todos.value.push(newTodo)
  text.value = ''
}

const deleteTodo = (i: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== todos.value[i].id)
}

const confirmed = (index: number) => {
  todos.value[index].done = !todos.value[index].done
}
</script>

<template>
  <div class="container">
    <h1 class="title">今日やること</h1>
    <div class="input-warp">
      <input type="text" class="input" v-model="text" />
      <Button
        @click="addTodo"
        :color="text ? '#008CFF' : '#c1c1c1'"
        :isDisable="!text"
        :cursor="!!text"
        >追加</Button
      >
    </div>

    <ul class="todo-ul">
      <li class="todo-wrap" v-for="(todo, index) in todos" :key="todo.id">
        <span class="todo" :class="todo.done && 'confirmedTodo'">{{ todo.text }}</span>
        <Button color="#FF3700" @click="deleteTodo(index)">削除</Button>
        <Button
          @click="confirmed(index)"
          :color="todo.done ? '' : '#008CFF'"
          :text-decoration="todo.done ? 'line-through' : ''"
          >完了</Button
        >
      </li>
    </ul>
  </div>
</template>

<style scoped>
.container {
  width: 375px;
  position: absolute;
  top: 50%;
  left: 50%;
  translate: -50% -50%;
  background: #ffffff;
  box-shadow: 0px 6px 6px #0000001a;
  border-radius: 24px;
  padding: 24px;
  box-sizing: border-box;
}

.title {
  text-align: left;
  font: normal normal normal 24px/41px Hiragino Maru Gothic ProN;
  letter-spacing: 0px;
  color: #000000;
  margin-bottom: 32px;
}

.input-warp {
  display: flex;
  gap: 20px;
  margin-bottom: 32px;
}

.input {
  width: 250px;
  height: 32px;
  background: #ffffff;
  border: 1px solid #cdcdcd;
  border-radius: 4px;
  box-sizing: border-box;
}

.todo-ul {
  margin: 0;
  padding: 0;
}

.todo-wrap {
  display: flex;
  gap: 20px;
  padding-bottom: 8px;
  border-bottom: 1px solid #cdcdcd;
}

.todo-wrap:not(:first-child) {
  margin-top: 16px;
}

.todo {
  flex: 1;
}

.confirmedTodo {
  text-decoration: line-through;
}
</style>

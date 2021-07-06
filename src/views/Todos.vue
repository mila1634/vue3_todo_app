<template>
  <div class="container">

    <div class="wrapper">
      <div class="todo-list">
        <div class="todo-list-left">
          <div v-for="(todo, index) in todos" :key="index" class="added-wrapper" :class="{'done-bg' : todo.done}">
            <div class="added-text">
              <div class="added-text-todo">{{ todo.text }}</div>
              <div class="added-text-time">{{ todo.createdAt.toString() }}</div>
            </div>
            <div class="added-btns">
              <button class="delete" @click="removeTodo(index)" :class="{'done-bg' : todo.done}">&times;</button>
              <button v-if="!todo.done" class="done" @click="markAsDone(index)">&check;</button>
              <button v-else class="undone" @click="markAsUndone(index)" :class="{'done-bg' : todo.done}">&#8630;</button>
            </div>
          </div>
          <div v-if="todos.length === 0" class="done-wrapper">
            You dont have any task to do.
          </div>
        </div>

        <div class="todo-list-add">
          <div class="add-wrapper">
            <h2>Add a todo</h2>
            <input type="text" v-model="todoText" @keydown.enter="addTodo">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, reactive, ref } from "vue";

export default defineComponent({
  setup() {
    const todos = reactive([]);
    const todoText = ref("");

    function addTodo() {
      todos.unshift({
        text: todoText.value,
        createdAt: new Date(),
        done: false,
      });

      todoText.value = "";
    }

    function markAsDone(index) {
      todos[index].done = true;
    }

    function markAsUndone(index) {
       todos[index].done = false;     
    }

    function removeTodo(index) {
      if(!confirm("Are you sure?")) {
        return;
      }

      todos.splice(index, 1);
    }

    return {
      todos,
      todoText,
      addTodo,
      markAsDone,
      markAsUndone,
      removeTodo,
    }
  }
})
</script>
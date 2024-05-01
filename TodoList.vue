<template>
    <div class="todo-list">
      <h1>Todo List</h1>
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo">
      <ul>
        <li v-for="(todo, index) in todos" :key="index" class="todo-item">
          <input margin-right:10px type="checkbox" :checked="todo.done" @change="toggleDone(todo)">
          <span class="todo-number">{{ index + 1 }}</span>
          <span :class="{ 'done': todo.done }">{{ todo.text }}</span>
        </li>
      </ul>
      <div class="actions">
        <button class="mark-done" @click="toggleMarkAllDone">Mark All Done</button>
        <button class="delete-all" @click="deleteAll">Delete All</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TodoList',
    data() {
      return {
        newTodo: '',
        todos: [],
        allDone: false // Track whether all items are marked as done
      };
    },
    methods: {
      addTodo() {
        if (this.newTodo.trim() !== '') {
          this.todos.push({ text: this.newTodo, done: false });
          this.newTodo = '';
        }
      },
      removeTodo(index) {
        this.todos.splice(index, 1);
      },
      toggleDone(todo) {
        todo.done = !todo.done;
      },
      toggleMarkAllDone() {
        if (this.allDone) {
          this.todos.forEach(todo => todo.done = false);
        } else {
          this.todos.forEach(todo => todo.done = true);
        }
        this.allDone = !this.allDone;
      },
      deleteAll() {
        this.todos = [];
      }
    }
  };
  </script>
  
  <style scoped>
  .todo-list {
    background-color: #41B883; 
    padding: 20px;
    border-radius: 10px;
  }
  
  .todo-item {
    display: flex;
    align-items: center;
    padding: 10px;
    margin-bottom: 10px;
    background-color: #f2f2f2; 
    border-radius: 5px;
  }
  
  .todo-number {
    margin-right: 20px;
    font-weight: bold;
  }
  
  .done {
    text-decoration: line-through;
  }
  
  .actions {
    margin-top: 20px;
  }
  
  .actions button {
    margin-right: 10px;
    background-color: #333; 
    color: #fff;
    border: none;
    border-radius: 20px;
    padding: 5px 10px;
    cursor: pointer;
  }
  </style>
  
<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" v-on:status-changed="statusChanged"/>
  </div>
</template>

<script>
import Header from "./components/layouts/Header.vue";
import Todos from "./components/Todos.vue";
import AddTodo from "./components/AddTodo.vue";

export default {
  name: "app",
  components: {
    Header,
    AddTodo,
    Todos
  },
  methods: {
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(f => f.id !== id);
    },
    statusChanged(todo) {
      this.$forceUpdate();
    }
  },
  data() {
    return {
      todos: []
    };
  },
  created() {
    // called after component has been loaded
    let fromStorage = localStorage.getItem("todos");
    if (fromStorage) {
      this.todos = JSON.parse(fromStorage);
    }
  },
  updated() {
    // called after any state has changed
    localStorage.setItem("todos", JSON.stringify(this.todos));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>

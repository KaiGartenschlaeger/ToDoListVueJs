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
    deleteTodo(todo) {
      this.todos = this.todos.filter(f => f.id !== todo.id);
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
ul.list-group.list-group-flush li:first-child {
  border-top: none;
}
ul.list-group.list-group-flush li:last-child {
  border-bottom: none;
}
</style>

<template>
  <div class="container pl-2 pr-2">
    <div class="progress mt-2 mb-2" style="height:1px" v-if="todos.length > 0">
      <div
        class="progress-bar"
        role="progressbar"
        v-bind:class="{'bg-success':allDone}"
        v-bind:style="{width:percentageDone + '%'}"
      ></div>
    </div>
    <div class="mt-3">
      <h5 v-if="todos.length > 0">
        In Progress
        <small>
          <span class="badge badge-secondary">{{todosInProgress.length}}</span>
        </small>
      </h5>
      <ul class="list-group list-group-flush" v-if="todos.length > 0">
        <template v-for="todo in todosInProgress">
          <TodoItem
            v-bind:key="todo.id"
            v-bind:todo="todo"
            v-bind:removeable="false"
            v-on:del-todo="$emit('del-todo', todo)"
            v-on:status-changed="$emit('status-changed', todo)"
          />
        </template>
      </ul>
      <div v-if="todos.length > 0 && todosInProgress.length === 0">
        <small class="text-muted">Lucky Guy... You've all done!</small>
      </div>
      <div v-if="todos.length === 0">
        <small class="text-muted">This is an empty place. Try to add some tasks...</small>
      </div>
    </div>
    <div class="mt-3" v-if="todosDone.length > 0">
      <h5>
        Done
        <small>
          <span class="badge badge-secondary">{{todosDone.length}}</span>
        </small>
      </h5>
      <ul class="list-group list-group-flush">
        <template v-for="todo in todosDone">
          <TodoItem
            v-bind:key="todo.id"
            v-bind:todo="todo"
            v-bind:removeable="true"
            v-on:del-todo="$emit('del-todo', todo)"
            v-on:status-changed="$emit('status-changed', todo)"
          />
        </template>
      </ul>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import _ from "lodash";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  computed: {
    completedCount: function() {
      return this.todos.filter(todo => todo.completed).length;
    },
    inProgressCount: function() {
      return this.todos.length - this.completedCount;
    },
    absoluteCount: function() {
      return this.todos.length;
    },
    allDone: function() {
      return this.completedCount >= this.absoluteCount;
    },
    percentageDone: function() {
      return Math.round((this.completedCount / this.absoluteCount) * 100);
    },
    percentageInProgress: function() {
      return 100 - this.percentageDone;
    },
    orderedTodos: function() {
      return _.orderBy(this.todos, "completed");
    },
    todosInProgress: function() {
      return this.todos.filter(todo => !todo.completed);
    },
    todosDone: function() {
      return this.todos.filter(todo => todo.completed);
    }
  },
  props: ["todos"]
};
</script>

<style scoped>
</style>

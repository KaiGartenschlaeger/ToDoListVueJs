<template>
  <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
    <p>
      <input type="checkbox" 
        v-bind:id="'item_' + todo.id" 
        v-bind:checked="todo.completed"
        v-on:change="markComplete">&nbsp;
      <label v-bind:for="'item_' + todo.id">{{todo.title}}</label>

      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
      markComplete() {
          this.todo.completed = !this.todo.completed;
      }
  }
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: #ccc dotted;
}

.todo-item.is-completed label {
  text-decoration: line-through;
  color: #aaa;
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>

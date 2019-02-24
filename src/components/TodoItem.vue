<template>
  <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
    <p>
      <input
        type="checkbox"
        v-bind:id="'item-' + todo.id"
        v-bind:checked="todo.completed"
        v-on:change="markComplete"
      >&nbsp;
      <label v-bind:for="'item-' + todo.id">{{todo.title}}</label>
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
      this.$emit('status-changed', this.todo);
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
  color: #aaa;
  text-decoration: line-through;
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

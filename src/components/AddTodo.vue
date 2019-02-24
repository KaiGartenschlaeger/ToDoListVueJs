<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" v-model="title" placeholder="Add todo..">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>

<script>
import uuid from "uuid";

export default {
  name: "AddTodo",
  methods: {
    addTodo(e) {
      e.preventDefault();

      if (!this.title || this.title.trim().length === 0) {
        return;
      }

      // create todo
      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false
      };

      // send up to parent
      this.$emit("add-todo", newTodo);

      // reset form
      this.title = "";
    }
  },
  data() {
    return {
      title: ""
    };
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>

<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" v-model="title" placeholder="Add todo..">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  methods: {
    addTodo(e) {
        e.preventDefault();

        // create todo
        const newTodo = {
            title: this.title
        };

        // send up to parent
        this.$emit('add-todo', newTodo);

        // reset form
        this.title = '';
    }
  },
  data() {
      return {
          title: ''
      }
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

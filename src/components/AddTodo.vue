<template>
    <form @submit="addTodo">
        <div class="container pl-2 pr-2 pt-2">
            <div class="row">
                <div class="col-md-12">
                    <div class="input-group">
                        <input
                            type="text"
                            name="title"
                            v-model="title"
                            placeholder="Enter the task description..."
                            class="form-control"
                        >
                        <div class="input-group-append">
                            <input type="submit" value="Add" class="btn btn-primary btn-block">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </form>
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
</style>

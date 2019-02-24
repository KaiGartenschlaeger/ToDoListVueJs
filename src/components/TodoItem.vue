<template>
    <li
        @click="markComplete"
        class="list-group-item d-flex justify-content-between align-items-center todo-item p-0 pt-2 pb-2"
        v-bind:class="{'completed':todo.completed}"
    >
        <small>
            <span class="title pr-1">{{todo.title}}</span>
        </small>
        <font-awesome-icon
            icon="trash"
            class="text-secondary"
            v-if="removeable"
            @click="$emit('del-todo', todo.id)"
        />
    </li>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo", "removeable"],
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
            this.$emit("status-changed", this.todo);
        }
    }
};
</script>

<style scoped>
li.todo-item {
    cursor: pointer;
}

li.todo-item.completed .title {
    color: #b3b3b3;
    text-decoration: line-through;
}
</style>

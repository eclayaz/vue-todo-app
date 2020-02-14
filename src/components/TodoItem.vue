<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <input class="complete-check" type="checkbox" v-on:change="markComplete">
        <p>{{todo.title}}</p>
        <button class="del" @click="$emit('del-todo', todo.id)">x</button>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: [
        "todo"
    ],
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style scoped>
  .todo-item {
    display: flex;
    align-items: center;
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .is-complete {
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
    margin-left: auto;
  }
  .complete-check {
    margin-right: 12px;
  }
</style>
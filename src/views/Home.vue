<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todosD="todosD" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>

import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todosD: []
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(rest => {this.todosD = this.todosD.filter(todo => todo.id != id); console.log(rest.data)})
      .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo;

      axios.post(
        'https://jsonplaceholder.typicode.com/todos', 
        { title, completed}
      )
      .then(rest => this.todosD = [...this.todosD, rest.data])
      .catch(err => console.log(err));
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then( res => this.todosD = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
</style>

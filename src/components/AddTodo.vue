<template>
    <form @submit="addTodo">
        <input type="text" v-model="title" name="Title" placeholder="Add Todo...">
        <input type="submit" value="Submit" class="btn">
    </form>
</template>

<script>

export default {
    name: "AddTodo",
    data(){
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            
            const newTodo = {
                title: this.title,
                completed: false
            }

            this.$emit('add-todo', newTodo);

            this.title = '';
        }
    }
}
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
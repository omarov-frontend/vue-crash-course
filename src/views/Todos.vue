<template>
  <div>
    <h2>Todo Shamil</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo 
      @add-todo="AddTodo"
    />
    <hr>
    <Loader v-if="loading" />
      <TodoList
        v-else-if="todos.lenght"
        v-bind:todos="todos"
        @remove-todo="removeTodo"
      />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'app',
  data () {
    return {
      todos: [],
      loading: true
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    .then(response => response.json())
    .then(json => {
      setTimeout(() => {
        this.todos = json
        this.loading = false
      }, 1000)
    })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    AddTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList, AddTodo, Loader
  }
}
</script>
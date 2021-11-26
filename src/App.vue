<template>
  <AddTodo v-on:add-todo="addTodo"/>
  <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
</template>

<script>
import axios from 'axios'
import Todos from './components/Todos'
import AddTodo from './components/AddTodo.vue'

export default {
  name: 'App',
  components: {
    Todos,
    AddTodo
  },
  data(){
    return {
      todos: []
    }
  },
  methods: {
    addTodo(newTodo) {
      const { title, completed } = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(error => {
        return Promise.reject(error)
      })
    },
    deleteTodo(id) {
      // this.todos = this.todos.filter(todo => todo.id !== id)
      axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
      .then(res => {
        this.todos = this.todos.filter(todo => todo.id !== id)
        return res
      })
      .catch(err => {
        return Promise.reject(err)
      })
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(error => {
      return Promise.reject(error)
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

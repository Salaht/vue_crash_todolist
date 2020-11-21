<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from 'axios';

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    //function
    return {
      //return array of objects
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      // filter loops trough condition returns an array
      // return everthing but that ID
      axios.delete(`http://jsonplaceholder.typicode.com/todos/${id}
      `)
      // eslint-disable-next-line no-unused-vars
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      // spread opirator copy whats in the todos and add to it
      // pull out some data
      const { title, completed } = newTodo;

      axios.post('http://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));

    }
  },
  created() {
    // fetch api/axios / it wil return a promise use .then
    // this can be a backend api node/expres/python/flask/jango
    axios.get('http://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
</style>

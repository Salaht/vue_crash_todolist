<template>
  <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">

    <p>
      <!-- added a change event -->
      <input type="checkbox" v-on:change="markComplete">
      {{todo.title}}
      <button @click="$emit('del-todo', todo.id)" class="del">X</button>
      </p>
      
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  // object of methods
  methods: {
    markComplete() {
      // je zet hem op wat de huidige value niet is
      this.todo.completed = !this.todo.completed;
    }
  }
}
</script>

<style scope>
.todo-item {
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
}
</style>

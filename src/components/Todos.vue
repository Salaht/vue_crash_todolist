<template>
    <div>
        <div  v-bind:key="todo.id" v-for="todo in todos">
                <!-- voor elke todo item bind je hem aan todo -->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)" />
        </div>
    </div>
</template>

<script>
import TodoItem from './Todoitem';

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    // je gebruikt v-bind om die data uit de App component te halen
    props: ["todos"]
}
</script>

<style scoped>

</style>
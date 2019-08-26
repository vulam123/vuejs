<template>
    <div>
        <h1>To do</h1>
        <div v-bind:key="todo.id" v-for="todo in list">
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)"/>
        </div>
    </div>
</template>
<script>

import TodoItem from './TodoItem.vue';
export default {
    name:"Todos",
    components:{
        TodoItem
    },
    props:["list"]
}
</script>
<style scoped>

</style>
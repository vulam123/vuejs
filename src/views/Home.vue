<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:list="todos" v-on:del-todo="deleteTodo"/>
   
  </div>
</template>

<script>
import Todos from '../components/Todos'
import AddTodo from '../components/AddToDo'
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data(){
    return {
      todos : []
    }
  },
  methods:{
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`).then(res=>{
        this.todos = this.todos.filter(todo => todo.id!==id);
      }).catch(err=>console.log(err))
    },
    addTodo(newTodo){
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title:newTodo.title,
        completed: newTodo.completed
      }).then(res=>{
        this.todos = [...this.todos,res.data]
      }).catch(err=>console.log(err))
      this.todos = [...this.todos,newTodo]
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10').then(res=>{
      this.todos = res.data;
    }).catch(err=>console.log(err))
  }
}
</script>

<style>

</style>

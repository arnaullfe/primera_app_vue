<template>
  <div>
    <div id="header">
      <Search v-on:query-change="querySearch"/>
    </div>
    <div id="main-container">
      <h2>Todos</h2>
      <TodoAdd v-on:add-todo="addTodo"/>
      <Todos v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo"/>
    </div>
  </div>
</template>

<script>
import Search from './components/Search'
import Todos from './components/Todos'
import TodoAdd from './components/TodoAdd'

export default {
  name: 'App',
  components: {
    Todos,TodoAdd, Search
  },
  data(){
    return {
      todos: [
        {
        id: 0,
        title: 'Comprar cena',
        completed: false
        },
         {
        id: 1,
        title: 'zbox',
        completed: true
        },
         {
        id: 2,
        title: 'test',
        completed: false
        },
        {
        id: 3,
        title: 'jugar al rocket league',
        completed: true
        }
      ],
      copyTodos: []
    }
  },
  created(){
    this.copyTodos = this.todos;
  },
  methods: {
    deleteTodo(id){
      this.todos = this.todos.filter((element)=>{return element.id!=id});
      this.copyTodos = this.todos;
    },
    addTodo(todo){
      this.todos.push(todo);
      this.copyTodos = this.todos;
    },
    querySearch(query){
      this.copyTodos = this.todos.filter((element)=>{ return element.title.trim().includes(query.trim())})
    }
  }
}
</script>

<style>
body{
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1.5em;
  padding: 0;
  margin: 0;
}

#main-container{
  border: solid 1px #ccc;
  width: 600px;
  margin: 100px auto;
}

#header{
  background: black;
  padding: 10px;
}

h2{
  padding: 0 10px;
}
</style>

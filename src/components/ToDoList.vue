<template>
  <div class="container">
    <p>Completed Tasks:{{todos.filter(todo=>{return todo.done == true}).length}}</p>
    <p>Pending Tasks:{{todos.filter(todo=>{return todo.done == false}).length}}</p>
    <my-todo 
    v-for="(todo, index) in todos" 
    :todo="todo"
    v-on:delete-todo="deleteTodo" 
    v-on:complete-todo="completeTodo"
    :key="index"
    v-on:hide-form="editTodo"></my-todo>
  </div>
</template>
<script>
import ToDo from './ToDo.vue'
export default {
  props:['todos']
  ,components:{
    MyTodo:ToDo
  },
  methods:{
    deleteTodo(todo){
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
      var datavlaue = this.todos;
      var todostr = JSON.stringify(datavlaue);
      localStorage.setItem('data', todostr);
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      var datavlaue = this.todos;
      var todostr = JSON.stringify(datavlaue);
      localStorage.setItem('data', todostr);
    },
    editTodo(todo){
      const todoIndex = this.todos.indexOf(todo);
      var gettodo = localStorage.getItem('data');
      var localtodo = JSON.parse( gettodo );
      localtodo[todoIndex].title = todo.title;
      localtodo[todoIndex].project = todo.project;
      localtodo[todoIndex].done = false;
      var todostr = JSON.stringify(localtodo);
      localStorage.setItem('data', todostr);
      window.location.reload();
    }
  }
}
</script>
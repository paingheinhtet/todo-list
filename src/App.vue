<template>
  <div id="app">
    <h1>My Vue Todo</h1>
    <hr>
    <to-do v-bind:todos='todos'></to-do>
    <create-todo v-on:add-todo="addTodo"></create-todo>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList'
import CreateToDo from './components/CreateToDo'
export default {
  components:{
    ToDo: ToDoList,
    createTodo:CreateToDo,
  },
  data(){
    return{
      todos:[{
        title:'Day Goals',
        project:'Learning New Technology',
        done:true
      },
      {
        title:'Week Goals',
        project:'Get New Friends',
        done:false
      },
      {
        title:'Year Goals',
        project:'Become A Professional Programmer',
        done:false
      },
      ],
    }
  },
  methods:{
    addTodo(data){
      this.todos.push(data);
      var datavlaue = this.todos;
      var todostr = JSON.stringify(datavlaue);
      localStorage.setItem('data', todostr);
    }
  },mounted:function(){
    if(localStorage.getItem('data')!=null){
      var gettodo = localStorage.getItem('data');
      this.todos = JSON.parse( gettodo );
    }else{
      var datavlaue = this.todos;
      var todostr = JSON.stringify(datavlaue);
      localStorage.setItem('data', todostr);
    }
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
</style>

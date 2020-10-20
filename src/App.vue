<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodoParent"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeTodo="removeTodoParent"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  name : 'app',
  components:{
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  },
  data(){
    return {
      todoItems : []
    }
  },
  methods : {
    addTodoParent(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodoParent(todoItem, idx){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created(){
    if(localStorage.length > 0){
        for(let i = 0; i<localStorage.length; ++i){
            this.todoItems.push(localStorage.key(i));
        }
    }
  }
}
</script>

<style>
    body{
        text-align: center;
        background-color: #F6F6F8;
    }
    input{
        border-style: groove;
        width: 200px;
    }
    button{
        border-style: groove;
    }
    .shadow{
        box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.3);
    }
</style>

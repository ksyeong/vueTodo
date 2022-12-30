<template>
  <todo-list v-bind:propsdata="todoLists" v-on:addTodoItem="addTodoList"></todo-list>
</template>

<script>
import TodoList from "./components/TodoList.vue"
export default {
  data:function(){
    return{
      todoLists: []
    }
  },
  methods:{
    addTodoList:function(todoItem){
      let obj = {complated: false , item: todoItem}
      localStorage.setItem(todoItem,JSON.stringify(obj));
      this.todoLists.push(obj)
    }
  },
  created: function(){
    if(this.todoLists !== ""){
      for(let i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== ""){
          this.todoLists.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
            }
        }
    },
  components:{
    "todo-list": TodoList
  }
}
</script>

<style>
body{
  background-color: rgb(255, 247, 238);
}
</style>
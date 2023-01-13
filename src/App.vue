<template>
  <div>
    <todo-list v-bind:propsdata="todoLists" v-on:addTodoItem="addTodoList" v-on:removeItem="removeOneItem" ></todo-list>
    <todo-footer v-on:clear="removeAllItem"></todo-footer>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue"
import TodoFooter from "./components/TodoFooter.vue"
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
    },
    removeOneItem: function(todoItem,index){
      localStorage.removeItem(todoItem.item);
      this.todoLists.splice(index ,1) 
    },
    removeAllItem: function(){
      localStorage.clear();
      this.todoLists = [];
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
    "todo-list": TodoList,
    "todo-footer":TodoFooter
  }
}
</script>

<style>
body{
  background-color: rgb(255, 247, 238);
}
</style>
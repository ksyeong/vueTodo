<template>
    <div class="container">
        <h1>Todo List</h1>
        <div class="subContainer shadow inputWrap">
            <input type="text" v-model="todoText" v-on:keyup.enter="addTodo">
            <button v-on:click="addTodo" class="inputBtn">+</button>
        </div>
        <div class="subContainer">
            <ul>
                <li v-for="todoList in propsdata" v-bind:key="todoList.item" class="shadow">{{ todoList.item }}</li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    props:["propsdata"],
    data: function(){
            return {
                todoText: "",
                todoLists: []
        }
    },
    methods:{
        addTodo: function(){
            let obj = {complated: false , item: this.todoText}
            localStorage.setItem(this.todoText, JSON.stringify(obj));
            this.$emit("addTodoItem",this.todoText)
            this.todoText = "";
        }
    }
}
</script>

<style scoped>
.container{
    margin: 0 auto;
    height: 100vh;
    width: 80vw;
    text-align: center;
}
.inputWrap{
    display: flex;
    background-color: white;
    border-radius: 5px;
    overflow: hidden;
}
input{
    width: 90%;
    box-sizing: border-box;
    line-height: 50px;
    border: none;
    font-size: 1.2em;
}
input:focus{
    outline: none;
}
.inputBtn{
    width: 10%;
    height: 50px;
    box-sizing: border-box;
    background: radial-gradient(#a5f5be,#eeee23);
    font-size: 36px;
}
ul{
    list-style-type: none;
    padding: 0;
}
li{
    width: 500px;
    line-height: 50px;
    min-height: 50px;
    height: 50px;
    background-color: white;
    margin: .9rem auto;
    border-radius: 5px;
}
/* common */
.shadow{
    box-shadow: 10px 10px 50px rgba(0, 0, 0, 0.03);
}
.subContainer{
    width: 500px;
    height: 50px;
    margin: 0 auto;
}
button{
    border: none;
    background-color: transparent;
}

</style>
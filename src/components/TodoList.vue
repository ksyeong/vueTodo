<template>
    <div class="container">
        <h1>Todo List</h1>
        <div class="subContainer shadow inputWrap">
            <input type="text" v-model="todoText" v-on:keyup.enter="addTodo" class="shadow">
            <button v-on:click="addTodo" class="inputBtn">+</button>
        </div>
        <div class="subContainer">
            <transition-group name="list" tag="ul">
                <li v-for="(todoList ,index) in propsdata" v-bind:key="todoList.item" class="shadow">{{ todoList.item }}
                <button v-on:click="removeTodo(todoList, index)" class="removeBtn">⌫</button>
                </li>
            </transition-group>
        </div>
        <Modal v-if="showModal" @close="showModal = false">
        <h3 slot="header">경고!
            <button class="closeModalBtn" @click="showModal = false">x</button>
        </h3>
        <p slot="body">내용이 입력되지 않았습니다.</p>
        </Modal>
    </div>

    
</template>

<script>
import Modal from "./co/AlertModal.vue"
export default {
    props:["propsdata"],
    data: function(){
            return {
                todoText: "",
                todoLists: [],
                showModal:false
            }
    },
    methods:{
        addTodo: function(){
            if(this.todoText !== ""){
                this.$emit("addTodoItem",this.todoText)
                this.todoText = "";
            }else{
                this.showModal = !this.showModal;
            }
        },
        removeTodo: function(todoItem,index){
            this.$emit("removeItem",todoItem,index)
        }
    },
    components:{
        Modal : Modal
    }
}
</script>

<style scoped>
.container{
    margin: 0 auto;
    height: fit-content;
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
    padding: 0;
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
    display: flex;
    width: 500px;
    line-height: 50px;
    min-height: 50px;
    height: 50px;
    background-color: white;
    margin: .9rem auto;
    border-radius: 5px;
    padding: 0 .9em;
    box-sizing: border-box;
}
.removeBtn{
    margin-left: auto;
    color: red;
    font-size: 24px;
}
/* common */
.subContainer{
    width: 500px;
    margin: 0 auto;
}
button{
    border: none;
    background-color: transparent;
    cursor: pointer;
}
.closeModalBtn{
    color: #42b983;
    font-weight: bold;
    font-size: 20px;
    text-align: center;
    line-height: 42px;
}
/* 리스트 트렌지션 효과 */
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>
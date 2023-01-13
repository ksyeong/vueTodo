<template>
    <div>
        <button class="allRemoveBtn" v-on:click="allRemoveTodo">모두지우기</button>
    </div>
</template>

<script>
export default {
    methods:{
        allRemoveTodo: function(){
            this.$emit("clear");
        }
    }
}
</script>

<style scoped>
div{
    display: flex;
    align-items: center;
    justify-content: center;
}
.allRemoveBtn{
    background-color: white;
    color: red;
    font-size: 20px;
    line-height: 2;
}
</style>
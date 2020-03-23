<template>
    <p v-bind:class = "{donetask: isDone}">
        <input type = "checkbox" v-on:cnange="change">
        <label> {{task.name}}</label>
        <button class="btnRemove" @click = "Remove(task)" >Remove</button>
    </p>
</template>

<script>
export default {
    name: "ToDoItem",
    props: ["task"],
    data() {
        return{
            isDone: false
        };
    },

    methods: {
        change(event) {
            if (event.target.checked == true){
                this.isDone = true;
                this.task.status = true;
            } else {
                this.isDone = false;
                this.task.status = false;
            }
            
        },

    }
};
</script>

<style scoped>
    .donetask {
        text-decoration: line-through;
        color: rgb(0, 0, 0);
    }
</style>
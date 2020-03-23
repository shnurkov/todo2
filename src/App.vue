<template>
  <div id="app">
    <h2 class="title"> Что бы сделать сегодня?</h2>
    <form @submit.prevent="onEnter">
      <input type="text" v-model = "taskItem" placeholder="Что там по делам?">
    </form>
    <ToDo v-for="(task, index) in tasks" :key = "index" :task="task"/>
    
    <button class="btnRemoveAll" @click = "RemoveAll(tasks)" >Remove All</button>
  </div>
</template>

<script>
/*eslint-disable*/
import ToDo from './components/ToDo.vue'

export default {
  el: 'App',
  components: {
    ToDo
  },
  data: function(){
    return{
      tasks: [
        {name: "Поесть", status: "false" },
        {name: "Поспать", status: "false"}
      ],
      taskItem: ""
    };
  },

  methods: {
    onEnter(event){
      if (this.taskItem){
        this.tasks.push ({name: this.taskItem, status: "false"});
      }
      this.taskItem = "";
    },

    RemoveAll: function(tasks){
      this.tasks.splice(0);
    }

  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.btnRemoveAll{
  margin-top: 10px;
}
</style>

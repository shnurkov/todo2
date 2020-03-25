<template>
  <div id="app">
    <h2 class="title">Что бы сделать сегодня?</h2>

    <form @submit.prevent="addTask">
      <input type="text" v-model="taskItem" placeholder="Что там по делам?" />
    </form>

    <!-- слушаем события changeStatus и removeTask и вызываем соответствующие функции -->
    <task
      v-for="(task, index) in tasks"
      :key="index"
      :task="task"
      :taskIndex="index"
      @changeStatus="changeStatus"
      @removeTask="removeTask"
    />

    <button class="btnRemoveAll" @click="removeAll">Remove All</button>
  </div>
</template>

<script>
// import ToDo from "./components/ToDo.vue";
// больше на 'task' похоже
import task from "./components/task";

export default {
  // el: "App", // не надо здесь
  components: {
    task
  },
  data() {
    return {
      tasks: [
        // { name: "Поесть", status: "false" },
        // { name: "Поспать", status: "false" }

        //почему status строка ?
        { name: "Поесть", status: false },
        { name: "Поспать", status: false }
      ],
      taskItem: ""
    };
  },

  methods: {
    /*
    onEnter(event) {
      if (this.taskItem) {
        this.tasks.push({ name: this.taskItem, status: "false" });
      }
      this.taskItem = "";
    },
    */

    // event ? он нам и нах*й не нужон
    // называй функции так, чтобы было понятно, что они делают onEnter -> addTask
    addTask() {
      if (this.taskItem) {
        this.tasks.push({ name: this.taskItem, status: false });
        this.taskItem = "";
      }
    },

    /*
    RemoveAll: function(tasks) {
      this.tasks.splice(0);
    }
    */

    // пиши в одинаковом стиле
    // не называй имена функций и переменных с большой буквы, большой буквой обозначают классы
    // tasks ? он и здесь нам не нужон
    removeAll() {
      this.tasks = []; //можно проще, без splice'oв
    },

    changeStatus(data) {
      this.tasks[data.index].status = data.status;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
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
.btnRemoveAll {
  margin-top: 10px;
}
</style>

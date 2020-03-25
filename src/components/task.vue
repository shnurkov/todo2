<template>
  <p v-bind:class="{'donetask': isDone}">
    <!-- чекбокс можно тоже связывать по v-model -->

    <!-- это так не работает, ты меняешь только локальный state, в App status как был false так и будет -->
    <!-- <input type="checkbox" v-on:cnange="change" /> -->
    <input type="checkbox" v-model="isDone" />
    <label>{{task.name}}</label>
    <button class="btnRemove" @click="remove">Remove</button>
  </p>
</template>

<script>
export default {
  name: "task",
  props: ["task", "taskIndex"], //taskIndex нам нужен чтобы обозначить с какой задачей мы работаем
  data() {
    return {};
  },

  // а вот и пример с computed :)
  computed: {
    isDone: {
      get() {
        return this.task ? this.task.status : false;
      },
      set(status) {
        // пропсы нельзя изменять, поэтому нам надо создать событие и изменить status уже в App.vue
        // инициируем событие changeStatus, которое можно прослушать на компоненте выше (App) и передаем туда какие то данные
        this.$emit("changeStatus", { status: status, index: this.taskIndex });
      }
    }
  },

  methods: {
    // это не будет работать :(
    // change(event) {
    //   if (event.target.checked == true) {
    //     this.isDone = true;
    //     this.task.status = true;
    //   } else {
    //     this.isDone = false;
    //     this.task.status = false;
    //   }
    // }

    remove() {
      // то же самое что и с changeStatus
      this.$emit("removeTask", this.taskIndex);
    }
  }
};
</script>

<style scoped>
.donetask {
  text-decoration: line-through;
  color: rgb(0, 0, 0);
}
</style>
<template>
  <div class="app">
    <h2 class="title">Список задач на сегодня</h2>

    <form @submit.prevent="addTask">
      <input type="text" v-model="taskItem" placeholder="Что там по делам?" />
    </form>
    <ToDo v-for="(task, index) in tasks" :key = "index" :task="task"/>
    
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
import task from "./components/task";

export default {
  name: 'App',
  components:{
    task
  },
  data(){
    return{
      tasks:[
        { name: "Поесть", status: false },
        { name: "Поспать", status: false }
      ],
       taskItem: ""
    };
  },
  methods:{
    addTask() {
      if (this.taskItem) {
        this.tasks.push({ name: this.taskItem, status: false });
        this.taskItem = "";
      }
    },
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
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
}
.btnRemoveAll {
  margin-top: 10px;
}
</style>

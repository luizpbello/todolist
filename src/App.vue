<template>
  <div id="app">
    <h1>Tarefas</h1>
    <TaskProgress :progress="progress" />
    <NewTask @taskAdded="addTask" />
    <TaskGrid
      @taskDeleted="deleteTask"
      @taskStateChanged="toggleStateChange"
      :tasks="tasks"
    ></TaskGrid>
  </div>
</template>

<script>
import TaskProgress from "./components/TaskProgress.vue";
import TaskGrid from "./components/TaskGrid.vue";
import NewTask from "./components/NewTask.vue";

export default {
  name: "App",
  components: {
    TaskGrid,
    NewTask,
    TaskProgress,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(task) {
      const sameTitle = (t) => t.title === task.title; // VERIFICA SE O TITLE JÁ CONSTA
      const reallyNew = this.tasks.filter(sameTitle).length == 0;
      if (reallyNew) {
        this.tasks.push({
          title: task.title,
          done: task.done || false,
        });
      }
    },
    deleteTask(i) {
      this.tasks.splice(i, 1);
    },
    toggleStateChange(i) {
      this.tasks[i].done = !this.tasks[i].done;
    },
  },
  created() {
    const json = localStorage.getItem("tasks");
    const array = JSON.parse(json);
    this.tasks = Array.isArray(array) ? array : [];
  },
  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter((t) => t.done).length;
      return Math.round((done / total) * 100) || 0;
    },
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
    },
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>

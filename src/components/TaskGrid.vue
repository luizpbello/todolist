<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <Task
        class="task-grid-item"
        v-for="(task, i) in tasks"
        :key="task.title"
        @taskDeleted = "$emit('taskDeleted', i)"
        @taskStateChanged = "$emit('taskStateChanged', i)"
        :task="task"
      >
        <task class="card">
          {{ task.title }}
        </task>
      </Task>
    </template>
    <p v-else class="no-task"> Sem tarefas hoje!</p>
  
  </div>
</template>

<script>
import Task from "./Task.vue";

export default {
  name: "TaskGrid",
  components: {
    Task,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.task-grid {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  height: 100vh;
  gap: 10px;
}

.no-task{
  color: #AAA;
  font-size:1.5rem;
}

@media screen and (max-width: 768px) {
  .task-grid {
    flex-direction: column;
    margin:10px;
    
  }
}


</style>

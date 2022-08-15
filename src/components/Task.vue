<template>
  <div
  @click="$emit('taskStateChanged', task)"
  class="task" :class="doneClass">
    <span @click.stop="$emit( 'taskDeleted', task)" class="close">x</span>
    <p>{{ task.title }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  computed: {
    doneClass() {
      return {
        done: this.task.done,
        pending: !this.task.done,
      };
    },
  },
};
</script>

<style scoped>
.task {
  position: relative;
  border-radius: 15px;
  padding: 20px;
  color: white;
  font-size: 1rem;
  font-weight: 700;
  box-sizing: border-box;
  cursor: pointer;
  user-select: none;
  width: 200px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.pending {
  background-color: rgb(253, 71, 71);
}

.done {
  background-color: rgb(99, 247, 99);
  text-decoration: line-through;
}

.pending .close {
  background-color: rgb(196, 22, 22);
}

.done .close {
  background-color: rgb(41, 138, 41);
}

.close {
  position: absolute;
  top: 10px;
  right: 10px;
  padding:5px;
  border-radius:5px;
  font-size: 0.5rem;
}

@media screen and (max-width: 768px) {
  .task {
    width: 290px;
  }
}
</style>

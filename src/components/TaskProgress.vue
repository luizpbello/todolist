<template>
  <div class="task-progress">
    <span class="progress-value"> {{ progress }} % </span>
    <div class="progress-bar" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<script>
export default {
  name: "TaskProgress",
  props: {
    progress: { type: Number, default: 0 },
  },
};
</script>

<style scoped>
.task-progress {
  position: relative;
  width: 80%;
  border: 1px solid white;
  border-radius: 5px;
  color: white;
  font-weight: 700;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-bar {
  position: absolute;
  border-radius: 5px;
  height: 100%;
  background-color: rgb(29, 255, 29);
  align-self: flex-start;
}

.progress-value {
  z-index: 1;
}

@media screen and (max-width: 768px) {
  .task-progress {
    width: 100%;
  }
}
</style>

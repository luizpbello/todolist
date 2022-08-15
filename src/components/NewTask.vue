<template>
  <div class="new-task">
    <input
      placeholder="Adicione uma nova tarefa..."
      class="form-element"
      v-model="title"
      @keydown.enter="add"
      type="text"
    />
    <button class="form-element" @click="add">+</button>
  </div>
</template>

<script>
export default {
  name: "NewTask",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    add() {
      this.$emit("taskAdded", { title: this.title });
      this.title = "";
    },
  },
};
</script>

<style scoped>
.new-task {
  margin: 35px;
  margin-bottom: -20px;
}

.form-element {
  padding: 10px;
  color: white;
  border: none;
  font-size: 1rem;
  outline: none;
}

input.form-element {
  width: 500px;
  background-color: #fff2;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

button.form-element {
  background-color: blueviolet;
  border-left: none;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  cursor: pointer;
}

@media screen and (max-width: 600px) {
  .new-task {
    margin: 20px;
  }
  input.form-element {
    width: 80%;
  }
}
</style>

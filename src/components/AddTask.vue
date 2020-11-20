<template>
  <form @submit.prevent="onAddTask">
    <div class="form-input">
      <div>
        <input
          id="task"
          type="text"
          placeholder="Enter a task..."
          v-model.trim="enteredTask"
        />
      </div>
      <div>
        <button class="add-btn">Add task</button>
      </div>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      enteredTask: ""
    };
  },
  methods: {
    onAddTask() {
      if (this.enteredTask) {
        this.$emit("add", this.enteredTask);
      }
      this.enteredTask = "";
    }
  }
};
</script>
<style scoped>
.form-input {
  display: flex;
  width: 100%;
  padding: 5px 10px;
}
input[type="text"] {
  width: 20rem;
  border-radius: 3px;
  border: none;
  padding: 9px;
  margin: 10px 5px;
  box-shadow: 0px 6px 8px 4px rgba(0, 0, 0, 0.2);
}
input[type="text"]:focus {
  outline-style: none;
}
::-webkit-input-placeholder {
  color: rgb(145, 146, 83);
  padding-left: 15px;
  font-family: candara light;
  font-size: 16px;
}
.add-btn {
  color: #fad507;
  background-color: #146268c9;
  border-radius: 3px;
  border: none;
  outline: none;
  padding: 8px;
  font-family: candara;
  font-size: 15px;
  box-shadow: 0px 6px 8px 4px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin: 10px 5px;
}
.add-btn:active {
  transform: translateY(1px);
}
</style>

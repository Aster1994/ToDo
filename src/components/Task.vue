<template>
  <div class="todo-item" :class="{ complete: task.completed }">
    <label>
      <input type="checkbox" v-model="checkbox" @change="onCheckingTask" />
      <span class="checkbox">
        <i class="fas fa-check-circle"></i>
      </span>
    </label>
    {{ task.title }}
    <button class="del-btn" type="button" @click="onRemove">
      <i class="fas fa-trash-alt"> </i>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      checkbox: false
    };
  },
  mounted() {
    this.checkbox = this.task.completed;
  },
  updated() {
    this.checkbox = this.task.completed;
  },
  methods: {
    onCheckingTask() {
      this.$emit("change-task", this.task);
    },
    onRemove() {
      this.$emit("remove", this.task);
    }
  }
};
</script>

<style scoped>
.todo-item {
  margin: 0 1rem;
  padding: 12px 12px 12px 0;
  border-bottom: 1px solid #5b5d5e71;
  font-size: 18px;
  color: rgba(247, 245, 242, 0.911);
  user-select: none;
}
.todo-item:first-child {
  border-top: 1px solid #5b5d5e71;
}
input[type="checkbox"] {
  display: none;
}
.checkbox {
  display: inline-block;
  font-size: 13px;
  color: #797a7abb;
  margin-right: 7px;
  cursor: pointer;
}
input[type="checkbox"]:checked + .checkbox {
  color: #832306;
}
.del-btn {
  float: right;
  background: none;
  border: none;
  outline: none;
  color: #146268c9;
  cursor: pointer;
}
.complete {
  text-decoration: line-through;
}
</style>

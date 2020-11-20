<template>
  <div class="container">
    <TaskHeader :countIncomplete="countIncomplete" @filter="onChangeFilter" />
    <AddTask @add="addingTask" />

    <div class="tasks" v-if="tasks.length > 0">
      <Task
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @remove="onRemove"
        @change-task="onCheckingTask"
      />
    </div>
  </div>
</template>

<script>
import TaskHeader from "@/components/TaskHeader";
import AddTask from "@/components/AddTask";
import Task from "./Task";

export default {
  props: {
    value: {
      type: Array,
      required: true
    }
  },
  components: {
    TaskHeader,
    AddTask,
    Task
  },
  data() {
    return {
      filter: "all"
    };
  },
  computed: {
    tasks: {
      get() {
        let tasks = this.value;
        switch (this.filter) {
          case "complete":
            tasks = tasks.filter(item => item.completed === true);
            break;
          case "inComplete":
            tasks = tasks.filter(item => item.completed === false);
            break;
        }
        return tasks;
      },
      set(val) {
        this.$emit("input", val);
      }
    },
    countIncomplete() {
      const tasks = this.tasks
        ? this.tasks.filter(item => item.completed === false)
        : 0;
      return tasks.length;
    }
  },
  methods: {
    onRemove(task) {
      const index = this.tasks.findIndex(item => item.id === task.id);
      this.tasks.splice(index, 1);
      this.$emit("remove", task);
    },
    onCheckingTask(task) {
      const index = this.tasks.findIndex(item => item.id === task.id);
      this.tasks[index].completed = !this.tasks[index].completed;
      this.$emit("change-task", task);
    },
    addingTask(title) {
      this.tasks.push({
        id: +new Date(),
        title: title,
        completed: false
      });
    },
    onChangeFilter(filter) {
      this.filter = filter;
    }
  }
};
</script>
<style scoped>
.container {
  width: 100%;
  padding: 2rem;
}
.tasks {
  display: flex;
  flex-direction: column;
  margin: 30px 0;
}
ul {
  list-style-type: none;
}
.complete {
  text-decoration: line-through;
}
</style>

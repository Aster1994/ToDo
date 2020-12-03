<template>
  <div id="app">
    <Tasks v-model="tasks" />
  </div>
</template>

<script>
import tasks from "@/assets/Tasks.js";
import Tasks from "./components/Tasks.vue";

export default {
  components: {
    Tasks
  },
  data() {
    return {
      tasks: tasks
    };
  }
};
</script>

<style>
@import url("https://use.fontawesome.com/releases/v5.13.0/css/all.css");
* {
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
}
body {
  background-color: #acafac94;
  max-width: 100%;
  margin: 0;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: candara;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-radius: 5px;
  background-color: #fac003c9;
  width: 60%;
  margin: 2rem 20%;
  box-shadow: 0px 6px 8px 4px rgba(0, 0, 0, 0.2);
}
@media only screen and (max-width: 50rem) {
  #app {
    width: 80%;
    margin: 2rem 10%;
  }
}
@media only screen and (max-width: 40rem) {
  #app {
    width: 100%;
    margin: 2rem 0;
  }
}
@media only screen and (max-width: 500px) {
  #app {
    width: 100%;
    margin: 0;
  }
}
</style>

<template>
  <header class="header">
    <div class="date">
      {{ getNow() }}
    </div>
    <div class="navbar">
      <div class="task-counter">{{ countIncomplete }} active tasks</div>
      <ul>
        <button
          @click="onChangeFilter('all')"
          :class="{ active: filter === 'all' }"
        >
          All task
        </button>
        <button
          @click="onChangeFilter('complete')"
          :class="{ active: filter === 'complete' }"
        >
          complete Tasks
        </button>
        <button
          @click="onChangeFilter('inComplete')"
          :class="{ active: filter === 'inComplete' }"
        >
          InComplete Tasks
        </button>
      </ul>
    </div>
  </header>
</template>
<script>
export default {
  props: {
    countIncomplete: Number
  },
  data() {
    return {
      filter: "all",
      today: "",
      intervalTime: null
    };
  },
  created() {
    this.intervalTime = setInterval(() => {
      this.getNow();
    }, 1000);
  },
  unmounted() {
    clearInterval(this.intervalTime);
  },
  methods: {
    getNow() {
      const now = new Date();
      const today =
        now.getDate() + "/" + (now.getMonth() + 1) + "/" + now.getFullYear();
      return today;
    },
    onChangeFilter(filter) {
      this.filter = filter;
      this.$emit("filter", this.filter);
    }
  }
};
</script>
<style scoped>
.header {
  height: 4.5rem;
  margin: 0;
  width: 100%;
}
@media only screen and (max-width: 500px) {
  .header {
    height: 7rem;
  }
}
.date {
  font-size: 27px;
  color: #024f55fb;
}
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 1.5rem;
}
@media only screen and (max-width: 500px) {
  .navbar {
    flex-direction: column;
    height: 3rem;
    align-items: flex-start;
  }
}
.task-counter {
  font-size: 15px;
  color: #832306;
  font-weight: bold;
}

ul {
  display: flex;
  list-style-type: none;
}

button {
  color: rgba(248, 242, 242, 0.74);
  margin-right: 10px;
  border-radius: 10px;
  cursor: pointer;
  border: none;
  background: transparent;
  font-family: candara;
  outline: none;
  font-family: candara;
  font-size: 17px;
}

button:active {
  transform: translateY(1px);
}
button.active,
button:focus {
  color: #024f55fb;
}
</style>

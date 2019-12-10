<template>
  <form id="app" @submit.prevent="createTask">
    <label class="label" for="task">Nueva tarea:</label>
    <input type="text" v-model="newTask" id="task" />
    <input type="submit" value="Crear tarea" />
    <ul>
      <li 
        v-for="(task, i) in tasks" 
        :key="'task' + i"
        :class="{completed: task.completed}"
      >
        {{ task.text }}
      </li>
    </ul>
  </form>
</template>

<script>
export default {
  data: () => ({
    newTask: "",
    tasks: []
  }),
  methods: {
    createTask() {
      let task = { text: this.newTask, completed: false };
      this.tasks.push(task);
      this.newTask = "";
      /* eslint-disable no-console */
      console.log(this.tasks);
      /* eslint-enable no-console */
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
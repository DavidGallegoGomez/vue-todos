<template>
  <div class="task-list">
    <form class="form" id="app" @submit.prevent="createTask">
      <label class="label" for="task">Nueva tarea:</label>
      <input class="input" type="text" v-model="newTask" id="task" />
      <input class="button" type="submit" value="Crear tarea" />
    </form>
    <br>
    <button v-if="tasks.length > 0 && allDone" @click="completeAllTask">ALL DONE</button>
    <button v-if="tasks.length > 0 && !allDone" @click="completeAllTask">ALL TODO</button>
    <ul class="list">
      <li 
        class="task"
        v-for="(task, i) in tasks" 
        :key="'task' + i"
        :class="{completed: task.completed}"
      >
        {{ task.text }}
        <button @click="completeTask(task.text)">DONE</button>
        <button @click="deleteTask(i)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: () => ({
    newTask: "",
    tasks: [],
    allDone: true
  }),
  methods: {
    createTask() {
      let task = { text: this.newTask, completed: false };
      this.tasks.push(task);
      this.newTask = "";
      /* eslint-disable no-console */
      console.log(this.tasks);
      /* eslint-enable no-console */
    },
    completeTask(taskText) {
      this.tasks
        .filter(task => task.text === taskText)
        .map(task => task.completed = !task.completed);
      // Si no fuera reactivo hay que usar "Vue.$set(array, indexOfItem, newValue)"
    },
    completeAllTask() {
      this.tasks.map(task => task.completed = this.allDone);
      this.allDone = !this.allDone;
    },
    deleteTask(index) {
      this.tasks.splice(index,1);
    }
  }
};
</script>

<style scoped>
.task-list {
  width: 800px;
  max-width: 100%;
  margin: 0px auto;
}
.form {
  background: white;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0px 10px 22px -1px rgba(0,0,0,0.25);
  margin-top: 10px;
}
.label {
  display: block;
  margin-bottom: 10px;
}
.input {
  height: 35px;
}
.button {
  margin-left: 20px;
  height: 35px;
  border: none;
  border-radius: 5px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, .2);
  background-color: #2ecc71;
  color: #ecf0f1;
  cursor: pointer
}
.list {
  margin-top: 40px;
}
.task {
  cursor: pointer;
  margin: 10px 0;
}
.completed {
  text-decoration: line-through;
  color: lightgrey;
}
</style>
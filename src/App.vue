<template>
  <div id="app">
    <h1>Daily Activity</h1>
    <input v-model="newTask" @keyup.enter="addTask">
    <button @click="addTask">add activity</button>
    <div v-for="(task, index) in tasks" :key="index">
      <span :class="{ completed: task.completed }">{{ task.name }}</span>
      <button @click="toggleCompletion(index)">mark as done</button>
      <button @click="deleteTask(index)">delete</button>
    </div>
    <button @click="showIncomplete">Tampilkan kegiatan yang belum selesai</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    }
  },
  methods: {
    addTask() {
      this.tasks.push({ name: this.newTask, completed: false });
      this.newTask = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleCompletion(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    showIncomplete() {
      this.tasks = this.tasks.filter(task => !task.completed);
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  
}

#app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  max-height: 900px;
  margin: 0 auto;
  padding: 20px;
  background-color: rgb(243, 151, 141);
  border-radius: 20px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

input, button {
  padding: 10px;
  font-size: 16px;
  border: none;
  margin-bottom: 10px;
}

button {
  background-color: purple;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: rgba(0, 255, 255, 0.636);
}

.completed {
  text-decoration: line-through;
  color: #422626;
}

.activity-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
}

.activity-item:last-child {
  border-bottom: none;
}

</style>

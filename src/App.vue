<template>
  <div id="app">
    <header>
      <h1>Daily Activity</h1>
      <nav>
        <button @click="showTodos">Todos</button>
        <button @click="showPosts">Post</button>
      </nav>
    </header>

    <div v-if="currentView === 'todos'">
      <h2>Todos</h2>
      <input v-model="newTask" @keyup.enter="addTask">
      <button @click="addTask">tambahkan kegiatan</button>
      <div v-for="(task, index) in tasks" :key="index">
        <span :class="{ completed: task.completed }">{{ task.name }}</span>
        <button @click="toggleCompletion(index)">Mark as Done</button>
        <button @click="deleteTask(index)">Delete</button>
      </div>
      <button @click="showIncomplete">tampilkan kegiatan yang belum selesai</button>
    </div>

    <div v-else-if="currentView === 'posts'">
      <h2>Posts</h2>
      <select v-model="selectedUser" @change="fetchUserPosts">
        <option v-for="user in users" :value="user.id" :key="user.id">{{ user.name }}</option>
      </select>
      <div v-for="(post, index) in userPosts" :key="index">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      currentView: 'todos',
      users: [],
      selectedUser: null,
      userPosts: []
    }
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => this.users = data)
        .catch(error => console.error('Error fetching users:', error));
    },
    fetchUserPosts() {
      if (this.selectedUser) {
        fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUser}`)
          .then(response => response.json())
          .then(data => this.userPosts = data)
          .catch(error => console.error('Error fetching user posts:', error));
      }
    },
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
    },
    showTodos() {
      this.currentView = 'todos';
    },
    showPosts() {
      this.currentView = 'posts';
    }
  }
}
</script>

<style scoped>
</style>

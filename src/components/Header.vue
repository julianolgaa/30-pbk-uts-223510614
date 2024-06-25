<!-- src/components/Header.vue -->
<template>
  <header>
    <router-link to="/">todolist</router-link>
    <router-link to="/posts">Postingan</router-link>
    <router-link to="/albums">Albums</router-link>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 10px 0;
  background-color: #f0f0f0; 
  border-radius: 8px;
}

router-link {
  color: #333; 
  text-decoration: none;
  font-size: 16px;
  padding: 10px 20px;
  border-radius: 4px;
  transition: background-color 0.3s, color 0.3s;
}

router-link:hover {
  background-color: #d9d9d9; 
}

router-link.active {
  background-color: #bfbfbf; 
}
</style>
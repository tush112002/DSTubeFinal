<template>
  <div>
    <header>
      <h1 class="tab">DSTube</h1>
      <div class="search-bar">
        <input v-model="search" @input="searchData" type="text" placeholder="Search" class="search-input">
        <button @click="searchData" class="search-button"><i class="fas fa-search"></i> Search</button>
      </div>
      <nav>
        <router-link to="/" class="nav-button home-button"> <i class="fas fa-home"></i> Home</router-link>
        <router-link to="/profile" class="nav-button profile-button"><i class="fas fa-user"></i> Profile</router-link>
      </nav>
    </header>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';
import '@fortawesome/fontawesome-free/css/all.css';

const emit = defineEmits(['search']); 
const search = ref('');

const searchData = () => {
  console.log("Search", search.value);
  emit('search', search.value); 
}
</script>

<style scoped>
#app {
  font-family: Arial, sans-serif;
}

header {
  background-color: #000000;
  color: #fff;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 2;
}

.tab {
  background-color: red;
  width: 100px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 18px;
  padding: 10px;
  border-radius: 4px;
}

nav {
  display: flex;
}

.search-bar {
  display: flex;
  align-items: center;
  margin: 0 auto;
}

.search-input {
  padding: 10px;
  font-size: 14px;
  width: 300px;
  margin-right: 10px;
  border-radius: 5px;
  color: #fff;
  
}

.search-button {
  padding: 10px 15px;
  font-size: 14px;
  border-radius: 5px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

.search-button:hover {
  background-color: #0056b3;
}

.nav-button {
  color: #fff;
  text-decoration: none;
  padding: 10px;
  border-radius: 5px;
  background-color: #007bff;
  cursor: pointer;
}

.home-button {
  margin-right: 20px;
}

.profile-button {
  margin-right: 50px;
}

.nav-button:hover {
  background-color: #0056b3;
}

.search-input {
  padding: 10px;
  font-size: 14px;
  width: 300px;
  margin-right: 10px;
  border-radius: 5px;
}

.search-button {
  padding: 10px 15px;
  font-size: 14px;
  border-radius: 5px;
}
</style>

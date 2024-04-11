<template>
  <div id="app">
    <Header @search="searchfunction" />
    <!-- <Profile/>
    <Home/> -->
    <!-- <View/> -->
    <router-view  :search="searchQuery"></router-view>
    <Footer/>
  </div>
</template>

<script setup>

import Header from './components/Home/Header.vue';
import Footer from './components/Home/Footer.vue';
import Profile from './components/Profile/Profile.vue'
import Home from './components/Home/Home.vue';
import View from './components/View/View.vue';



import { ref } from 'vue';

const searchQuery=ref('');

const searchfunction=(searchValue)=>{
    console.log("inside App js",searchValue);
    searchQuery.value=searchValue;
}
</script>


<style>
</style>

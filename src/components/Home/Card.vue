<template>
  <div>
    <router-link v-for="video in filterData" :key="video.id" :to="'/view/' + video.id" class="card-link">
      <div class="card">
          <img :src="video.imgSrc" :alt="'Card Image ' + video.id" class="card-image">
          <div class="card-details">
            <h3 class="card-title">{{ video.title }}</h3>
            <p class="card-views">Views: <span class="text-color">{{ video.views }}</span></p>
            <p class="card-desc">{{ video.desc }}</p>
            <p class="card-firstname"><span class="text-color">{{ video.creator.firstname }}</span></p>
            <p class="card-lastname"><span class="text-color">{{ video.creator.lastname }}</span></p>
          </div>
        </div>
      </router-link>
  </div>
</template>

<script setup>
import { ref, computed ,defineProps} from 'vue';
import Data from '../../assets/config/data.json';

const props = defineProps({
  search:{
    type:String,
    default:''
  }
})
const videolist = ref(Data);

const filterData = computed(() => {
  const res = videolist.value.filter(video => {
    return video.title.toLowerCase().includes(props.search.toLowerCase());
  });
    console.log('reseef',props.search);
    return res;
  });
</script>

<style scoped>
.card-link {
  text-decoration: none; 
  color : white;
}

.card {
  display: flex;
  margin: 20px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(255, 255, 255, 0.596);
  border: 1.5px solid rgb(255, 255, 255);
  transition: transform 0.2s ease-in-out;
}

.card:hover {
  box-shadow: 0 8px 16px rgba(255, 255, 255, 0.2);
  transform: translateY(-5px); 
}

.card-image {
  width: 300px;
  height: auto;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

.card-details {
  flex: 1;
  padding: 20px;
}

.card-title {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 10px;
}

.card-views {
  font-size: 14px;
  margin-bottom: 5px;
}

.text-color {
  color: rgb(255, 4, 4);
}

.card-desc,
.card-firstname,
.card-lastname {
  margin-bottom: 10px;
}

.card-desc {
  font-size: 16px;
}

.card-info {
  font-size: 14px;
}

.card:last-child {
  margin-bottom: 70px;
}
</style>

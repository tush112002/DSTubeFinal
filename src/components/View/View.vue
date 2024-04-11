<template>
  <div class="page">
    <div class="container">
      <div class="video-card">
        <div class="video-thumbnail">
          <iframe :src="video.videoSrc" :alt="'Card Image ' + video.id" allowfullscreen class="youtube-video" />
        </div>
        <div class="video-details">
          <h3 class="video-title">{{ video.title }}</h3>
          <p class="video-views">Views: {{ video.views }}</p>
          <p class="video-status" :class="[getStatusClass]">{{ getStatus }}</p>
          <div class="channel-info">
            <img :src="video.channelImgSrc" :alt="'Channel Image ' + video.id" class="channel-image">
            <div class="channel-details">
              <p class="channel-name">{{ video.creator.firstname }} {{ video.creator.lastname }}</p>
              <button @click="toggleSubscription" class="subscribe-button" :class="{ 'subscribed': isSubscribed }">
                {{ isSubscribed ? 'Subscribed' : 'Subscribe' }}
              </button>
            </div>
          </div>
          <div class="video-actions">
            <button @click="likeVideo" class="action-button like-button">
              <i class="fas fa-thumbs-up"></i>
              Like {{ likes }}
            </button>
            <button @click="dislikeVideo" class="action-button dislike-button">
              <i class="fas fa-thumbs-down"></i>
              Dislike
            </button>
            <button class="action-button share-button">
              <i class="fas fa-share"></i>
              Share
            </button>
          </div>
        </div>
        <input type="text" placeholder="Enter your comment" v-model="comment" class="comment-input">
        <button @click="submitComment" class="submit-button">Submit</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, reactive, computed } from 'vue';
import { useRoute } from 'vue-router';
import data from '../../assets/config/data.json';

import '@fortawesome/fontawesome-free/css/all.css';

const video = reactive({
  imgSrc: '',
  title: '',
  views: 0,
  channelImgSrc: '',
  creator: {
    firstname: '',
    lastname: ''
  }
});

const likes = ref(0);
const comment = ref('');
const isSubscribed = ref(false);

const likeVideo = () => {
  likes.value++;
};

const dislikeVideo = () => {
  if (likes.value > 0) {
    likes.value--;
  }
};

const toggleSubscription = () => {
  isSubscribed.value = !isSubscribed.value;
};

const submitComment = () => {
  if (comment.value.trim() !== '') {
    alert("Comment Added");
    console.log('Comment submitted:', comment.value);
    comment.value = '';
  } else {
    console.error('Comment cannot be empty');
  }
};

const route = useRoute();

onMounted(() => {
  const id = route.params.id;
  const fetchedVideo = data.find(item => item.id === id);
  Object.assign(video, fetchedVideo);
});

const getStatus = computed(() => {
  if (likes.value >= 15) {
    return 'Trending';
  } else if (likes.value >= 10) {
    return 'Popular';
  } else {
    return '';
  }
});

const getStatusClass = computed(() => {
  return getStatus.value.toLowerCase();
});
</script>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-grow: 1;
  margin-bottom: 80px;
}

.video-card {
  border: 2px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 100%;
  max-width: 50vw;
  display: flex;
  flex-direction: column;
  margin-top: 100px;
}

.video-thumbnail {
  position: relative;
  width: 100%;
  padding-top: 56.25%;
  overflow: hidden;
  border-radius: 8px;
}

.youtube-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: none;
}

.video-details {
  padding: 20px 0;
}

.video-title {
  font-size: 20px;
  margin-bottom: 10px;
}

.video-views {
  margin-bottom: 5px;
}

.video-status {
  margin-bottom: 10px;
  font-weight: bold;
  text-transform: uppercase;
}

.popular {
  background-color: #03b2f7;
  padding: 2px 6px;
  width: 82px;
}

.trending {
  background-color: #ffd700;
  padding: 2px 6px;
  width: 87px;
}

.video-actions {
  margin-bottom: 10px;
  margin-top: auto;
  margin-top: 20px;
}

.action-button {
  padding: 8px 16px;
  margin-right: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.like-button {
  background-color: #4caf50;
  color: white;
}

.dislike-button {
  background-color: #f44336;
  color: white;
}

.share-button {
  background-color: #008cba;
  color: white;
}

.channel-info {
  display: flex;
  align-items: center;
}

.channel-details {
  display: flex;
  align-items: center;
  flex-grow: 1;
  margin-right: 20px;
}

.channel-name {
  font-size: 18px;
  border: 1px solid black;
  padding: 4px;
}

.subscribe-button {
  padding: 8px 16px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-left: auto;
  transition: background-color 0.3s ease;
  /* Add transition */
}

.subscribe-button.subscribed {
  background-color: gray;
}

.subscribe-button:hover {
  background-color: #d32f2f;
}

.comment-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-bottom: 10px;
}

.submit-button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #0056b3;
}

.channel-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}
</style>

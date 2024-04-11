<template>
  <div class="page">
    <Header />
    <v-container class="container">
      <v-card class="profile-form">
        <h2 id="title" class="title">{{ isEditMode ? 'Update' : 'Enter' }} Profile Information</h2>
        <v-form class="form-container" @submit.prevent="saveOrUpdateProfile">
          <v-container>
            <v-text-field v-model="formData.name" label="Name" required></v-text-field>
            <v-text-field v-model="formData.email" label="Email" required></v-text-field>
            <v-text-field v-model="formData.phone" label="Phone" required></v-text-field>
            <v-text-field v-model="formData.password" label="Password" required type="password"></v-text-field>
          </v-container>
          <v-btn type="submit" class="save-button">{{ isEditMode ? 'Update' : 'Save' }}</v-btn>
        </v-form>
      </v-card>
    </v-container>
    <v-container class="container">
      <v-card class="profile-details-container">
        <v-container class="profile-details">
          <h2 id="title2" class="title2">Profile Details</h2>
          <v-container class="details">
            <p><strong>Name:</strong> {{ fullName }}</p>
            <p><strong>Email:</strong> {{ formData.email }}</p>
            <p><strong>Phone:</strong> {{ formData.phone }}</p>
          </v-container>
          <v-btn v-if="!isEditMode" @click="toggleEditMode" class="update-button">Update</v-btn>
        </v-container>
      </v-card>
    </v-container>
    <Footer />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const formData = ref({
  name: '',
  email: '',
  phone: '',
  password: ''
});

const isEditMode = ref(false);

const fullName = computed(() => {
  return formData.value.name;
});

const saveOrUpdateProfile = () => {
  if (isEditMode.value) {
    console.log('Updated Profile Data:', formData.value);
    isEditMode.value = false;
  } else {
    console.log('Saved Profile Data:', formData.value);
  }
};

const toggleEditMode = () => {
  isEditMode.value = true;
};
</script>

<style scoped>
.title{
  margin-left: 20px;
}

.title2 {
  margin-left: 15px;
}

.page {
  min-height: 100vh;
  justify-content: center;
  align-items: center;
}

.container {
  margin-top: 90px;
  max-width: 500px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 10px;
  margin-bottom: 5px; /* Adjusted margin-bottom */
  border: 1px solid #ccc;
}

.profile-form,
.profile-details-container {
  padding-top: 20px;
}

.form-container {
  margin-top: 15px;
}

.save-button{
  background-color:cyan;
}

.save-button,
.update-button {
  border-radius: 5px;
  cursor: pointer;
  margin: 20px auto;
  display: block;
}

.update-button {
  align-self: center;
  width: 100px;
  background-color: greenyellow;
}

.details p {
  margin-bottom: 10px;
}
</style>

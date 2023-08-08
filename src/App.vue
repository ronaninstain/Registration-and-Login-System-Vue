<script setup>
import { ref, reactive } from 'vue';

// Reactive data
const showLogin = ref(true);
const loggedIn = ref(false);
const loggedInUser = ref({});
const registerData = reactive({
  email: '',
  password: '',
});
const loginData = reactive({
  email: '',
  password: '',
});

// Simulated registration logic
function register() {
  loggedIn.value = true;
  loggedInUser.value = { email: registerData.email };
}

// Simulated login logic
function login() {
  loggedIn.value = true;
  loggedInUser.value = { email: loginData.email };
}

// Log out function
function logout() {
  loggedIn.value = false;
  loggedInUser.value = {};
}
</script>

<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white p-8 rounded shadow-md w-96">
      <h1 class="text-2xl font-semibold mb-4">Registration and Login</h1>

      <div v-if="!loggedIn">
        <form v-if="!showLogin" @submit.prevent="register" class="space-y-4">
          <h2 class="text-lg font-medium">Register</h2>
          <div>
            <label for="register-email" class="block text-sm font-medium">Email:</label>
            <input v-model="registerData.email" type="email" id="register-email" class="form-input w-full">
          </div>
          <div>
            <label for="register-password" class="block text-sm font-medium">Password:</label>
            <input v-model="registerData.password" type="password" id="register-password" class="form-input w-full">
          </div>
          <button type="submit"
            class="w-full bg-blue-500 text-white py-2 rounded hover:bg-blue-600 transition">Register</button>
          <p class="text-center mt-2">
            Already have an account? <a href="#" @click="showLogin = true" class="text-blue-500">Log in</a>
          </p>
        </form>

        <form v-if="showLogin" @submit.prevent="login" class="space-y-4">
          <h2 class="text-lg font-medium">Log in</h2>
          <div>
            <label for="login-email" class="block text-sm font-medium">Email:</label>
            <input v-model="loginData.email" type="email" id="login-email" class="form-input w-full">
          </div>
          <div>
            <label for="login-password" class="block text-sm font-medium">Password:</label>
            <input v-model="loginData.password" type="password" id="login-password" class="form-input w-full">
          </div>
          <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded hover:bg-blue-600 transition">Log
            in</button>
          <p class="text-center mt-2">
            Don't have an account? <a href="#" @click="showLogin = false" class="text-blue-500">Register</a>
          </p>
        </form>
      </div>

      <div v-else>
        <h2 class="text-lg font-medium mb-4">Welcome, {{ loggedInUser.email }}</h2>
        <button @click="logout" class="w-full bg-red-500 text-white py-2 rounded hover:bg-red-600 transition">Log
          out</button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>



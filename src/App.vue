<template>
  <nav>
    <router-link to="/" v-if="!isUserLoggedIn">Home</router-link>
    <router-link to="/about" v-if="!isUserLoggedIn">About</router-link>
    <router-link to="/services" v-if="!isUserLoggedIn">Services</router-link>
    <router-link to="/signup" v-if="!isUserLoggedIn">Signup</router-link>
    <router-link to="/login" v-if="!isUserLoggedIn">Login</router-link>
    <router-link to="/logout" v-if="isUserLoggedIn">Logout</router-link>
  </nav>
  <router-view/>
</template>

<!-- <script>
export default{
  computed: {
    isLoggedIn(){
      const authToken = localStorage.getItem('auth-token');
      return !!authToken;
    }
  }
}
</script> -->
<script setup>
  import { ref, onMounted, computed } from 'vue';

  const isLoggedIn = ref(false);

  onMounted(() => {
    isLoggedIn.value = !!localStorage.getItem('auth-token');
  })

  const isUserLoggedIn = computed(() => isLoggedIn.value);
  
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  padding: 14px 28px;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

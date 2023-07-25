<template>
    <div class="login-container">
        <h2>Login</h2>
            <form @submit.prevent="login">
                <label for="username">Username:</label>
                <input type="text" id="username" name="username" v-model="user.username" required>

                <label for="password">Pasword:</label>
                <input type="password" id="password" name="password" v-model="user.password" required>

                <input type="submit" value="Login">
            </form>
    </div>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { useRouter } from 'vue-router';
const user = ref({
    username: '',
    password: ''
})

const router = useRouter();

const login = async ()=> {
    try {
        const response = await axios.post('http://127.0.0.1:8000/api/login', user.value);
        console.log(response.data.token);
        const authToken = response.data.token;
        localStorage.setItem('auth-token', authToken)
        router.push({name: 'dashboard'});
    } catch (error) {
        console.log(error);
    }
}
</script>

<style>
    body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
}

.login-container {
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

form {
  display: flex;
  flex-direction: column;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input[type="text"],
input[type="password"] {
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

input[type="submit"] {
  padding: 10px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

input[type="submit"]:hover {
  background-color: #45a049;
}

</style>
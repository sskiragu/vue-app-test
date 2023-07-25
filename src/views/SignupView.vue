<template>
<div class="signup-container">
    <h2>Signup</h2>
    <form @submit.prevent="signup" method="POST">
      <label for="username">Username:</label>
      <input type="text" id="username" name="username" placeholder="Enter your username" v-model="username">

      <label for="email">Email:</label>
      <input type="email" id="email" name="email" placeholder="Enter your email" v-model="email">

      <label for="password">Password:</label>
      <input type="password" id="password" name="password" placeholder="Enter your password" v-model="password">

      <label for="confirm-password">Confirm Password:</label>
      <input type="password" id="confirm-password" name="confirm-password" placeholder="Confirm your password">

      <input type="submit" value="Signup">
    </form>
    <div class="login-options">
      <p>Already have an account? <a href="#">Login</a></p>
      <p><a href="#">Forgot Password?</a></p>
    </div>
</div>

</template>

<script>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

export default {
    // data(){
    //     return{
    //         input:{
    //             username: "",
    //             email: "",
    //             password: ""
    //         }
    //     }
    // },
    // methods: {
    //      signup(){
    //         console.log(this.input.username);
    //     }
    // }

    setup(){
        const username = ref('');
        const email = ref('');
        const password = ref('');
        const router = useRouter();

        const signup = async () => {
            try {
                await axios.post('http://127.0.0.1:8000/api/signup',{
                    username: username.value,
                    email: email.value,
                    password: password.value
                })
                router.push({ path: '/'})
                console.log('successful');
            } catch (error) {
                console.log(error);
            }
        }

        return {username, email, password, signup}
    }
}
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
}

.signup-container {
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
input[type="email"],
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

.login-options {
  margin-top: 20px;
  text-align: center;
}

.login-options a {
  text-decoration: none;
  color: #007bff;
}

.login-options a:hover {
  text-decoration: underline;
}

</style>

<template>
  <div class="register-container">
    <h2>Register</h2>
    <form @submit.prevent="register">
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" id="username" v-model="username" required>
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" id="password" v-model="password" required>
      </div>
      <div class="form-group">
        <label for="confirm-password">Confirm Password</label>
        <input type="password" id="confirm-password" v-model="confirmPassword" required>
      </div>
      <button type="submit">Register</button>
    </form>
    <p>
      Already have an account? <a href="#" @click.prevent="$emit('show-login')">Login</a>
    </p>
  </div>
</template>

<script>
import { users } from '../store/users';
import Swal from 'sweetalert2';

export default {
  data() {
    return {
      username: '',
      password: '',
      confirmPassword: ''
    };
  },
  methods: {
    register() {
      if (this.password !== this.confirmPassword) {
        Swal.fire({
          title: 'Error!',
          text: 'Passwords do not match!',
          icon: 'error',
          confirmButtonText: 'OK'
        });
        return;
      }
      if (users.find(user => user.username === this.username)) {
        Swal.fire({
          title: 'Error!',
          text: 'Username already exists!',
          icon: 'error',
          confirmButtonText: 'OK'
        });
        return;
      }
      users.push({ username: this.username, password: this.password });
      Swal.fire({
        title: 'Success!',
        text: `Registered as ${this.username}`,
        icon: 'success',
        confirmButtonText: 'OK'
      }).then(() => {
        this.$emit('show-login');
      });
    }
  }
};
</script>

<style scoped>
.register-container {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.form-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
}
input {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}
button {
  width: 100%;
  padding: 10px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
p {
  margin-top: 15px;
  text-align: center;
}
</style>

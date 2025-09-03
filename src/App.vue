<script>
import Login from './components/Login.vue'
import Register from './components/Register.vue'

export default {
  components: {
    Login,
    Register
  },
  data() {
    return {
      showLogin: true
    }
  }
}
</script>

<template>
  <div v-if="showLogin">
    <Login @show-register="showLogin = false" />
  </div>
  <div v-else>
    <Register @show-login="showLogin = true" />
  </div>
</template>

<style scoped>
</style>

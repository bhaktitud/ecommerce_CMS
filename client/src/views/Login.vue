<template>
    <div class="login-form" v-if="!loading">
        <form @submit.prevent="loginProcess" class="container border border-dark mt-3 rounded pb-4 pt-2 px-4 w-25 shadow">
            <div class="container form-group d-flex flex-column">
                <h1>Login</h1>
                <p>Please fill in this form to login.</p>
                <hr>
                <label for="email"><b>Email</b></label>
                <input v-model="email" type="text" placeholder="Enter Email" name="email" required>

                <label for="psw"><b>Password</b></label>
                <input v-model="password" type="password" placeholder="Enter Password" name="psw" required>

                <hr>
                <button type="submit" class="btn btn-primary loginbtn">login</button>
            </div>
            <div class="container signin">
                <p>Don't have an account? <router-link to="/register">Register</router-link>.</p>
            </div>
        </form>
    </div>
</template>

<script>
import { mapActions, mapState } from 'vuex'
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  computed: {
    ...mapState(['loading'])
  },
  methods: {
    ...mapActions(['onLogin']),
    loginProcess () {
      const { email, password } = this
      this.onLogin({ email, password })
    }
  },
  beforeRouteEnter (to, from, next) {
    if (localStorage.getItem('access_token')) {
      next('/dashboard')
    } else {
      next()
    }
  }
}
</script>

<style>
.login-form {
  margin-top: 5em;
}
</style>

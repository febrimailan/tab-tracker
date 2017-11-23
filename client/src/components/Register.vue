<template>
  <v-layout column>
    <v-flex xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar flat dense class="cyan" dark>
          <v-toolbar-title>Register</v-toolbar-title>
        </v-toolbar>
        <div class="pl-4 pr-4 pt-2 pb-2">
          <input class="blue lighten-4" type="email" name="email" v-model="email" placeholder="email" />
          <br>
          <br>
          <input class="blue lighten-4" type="password" name="password" v-model="password" placeholder="password" />
          <br>
          <br>
          <v-btn class="cyan" @click="register">Register</v-btn>
          <div class="error" v-html="error" />
        </div>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  watch: {
    email (value) {
      console.log('email has change', value)
    }
  },
  methods: {
    async register () {
      try {
        // console.log('register button was click', this.email, this.password)
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
      
    }
  },
  mounted () {
    // setTimeout(() => {
    //   this.email = 'Hello World'
    // }, 2000)
  }
}
</script>

<style scoped>
  .error {
    color: red;
  }
</style>

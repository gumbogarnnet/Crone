<template>
  <!-- Material form login -->
  

<div class="col-6 center">
    <div class="row d-flex justify-content-center mt-2">
    <i class="fas fa-user fa-10x"></i>
    </div>
  <form @submit.prevent="login">
    <p class="h4 text-center mb-4">Sign in</p>
    <div class="grey-text">
      <mdb-input label="Your email" icon="envelope" type="email" v-model="username"/>
      <mdb-input label="Your password" icon="lock" type="password" v-model="password"/>
    </div>
    <div class="text-center">
      <mdb-btn>Login</mdb-btn>
    </div>
    <p>Not a user <router-link to="/register">Register</router-link> </p>
  </form>
</div>
  <!-- Material form login -->
</template>
<script>
  import { mdbInput, mdbBtn } from 'mdbvue';
  export default {
    name: 'Basic',
    components: {
      mdbInput,
      mdbBtn
    },
methods: {
 login: function () {
   const { username, password } = this
   this.$store.dispatch(AUTH_REQUEST, { username, password }).then(() => {
     this.$router.push('/')
   })
 }
},
  }
  
</script>
<style scoped>
.center {
  margin: auto;
}
</style>

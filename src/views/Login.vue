<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <TheLogin></TheLogin>
  </div>
</template>

<script>
// @ is an alias to /src
import TheLogin from '@/components/TheLogin.vue'

export default {
  name: 'Login',
  components: {
    TheLogin
  }
}
</script>

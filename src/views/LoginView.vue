<template>
<v-container>
  <v-row>
    <v-col cols="12">
      <LoginForm/>
    </v-col>
  </v-row>
</v-container>
</template>

<script>
import LoginForm from '../components/Login.vue'
export default {
  components: {
    LoginForm
  }
}
</script>

<style>

</style>

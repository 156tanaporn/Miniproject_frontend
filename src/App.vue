<template>
  <v-app>
    <v-app-bar
      app
      dark
      color="blue"
    >
      <div class="d-flex align-center">
        <span class="mr-2" style="font-size: 20px;">Review Series </span>


      </div>

      <v-spacer></v-spacer>

      <v-btn
        text
        @click="goToHome()"
      >
        <span class="mr-2">Home</span>

      </v-btn>

      <v-btn
        text
        @click="goToRegister()"
      >
        <span class="mr-2">Register</span>

      </v-btn>

      <v-btn
        text
        @click="goToLogin()"
      >
        <span class="mr-2">Login</span>

      </v-btn>

    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
  methods: {
    goToLogin () {
      this.$router.push({ path: '/login' }).catch(() => {})
    },
    goToHome () {
      this.$router.push({ path: '/' }).catch(() => {})
    },
    goToRegister () {
      this.$router.push({ path: '/register' }).catch(() => {})
    }
  }

}
</script>

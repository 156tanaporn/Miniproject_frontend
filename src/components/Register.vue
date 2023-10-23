<template>

<v-container class="maxSize ">

            <div class="text-h3 text-center mb-10">Register</div>
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
        <div class="font-weight-medium">Username</div>
            <v-text-field
            v-model="username"
            :counter="10"
            :rules="nameRules"
            label="Enter username "
            required
            ></v-text-field>

        <div class="font-weight-medium">Password</div>
            <v-text-field
            v-model="password"
            :rules="passwordRules"
            label="Enter password"
            required
            ></v-text-field>
        <div class="font-weight-medium">Confirm password</div>
            <v-text-field
            v-model="confirmPassword"
            :rules="passwordRules"
            label="Enter confirm password"
            required
            ></v-text-field>
        <div class="font-weight-medium">Email contact</div>
            <v-text-field
            label="Enter email contact"
            ></v-text-field>

<div class="text-center">

            <v-btn
            color="primary"
            @click="something"
            href="/login"
            >
            Register
            </v-btn>
</div>
  </v-form>

</v-container>
</template>

<script>
export default {

}
</script>

<style>
.maxSize {
  max-width: 600px;
  height: 1000px;
}

</style>

<template>
  <v-container class="ma-5">
    <v-row justify="center">
      <v-col cols="12" sm="8" md="6">
        <v-card>
          <v-card-title class="headline">
            Review Series
          </v-card-title>
          <v-card-text>
            <v-form @submit="submitReservation">
              <v-textarea v-model="comment" label="comment"></v-textarea>
              <v-btn color="primary" type="submit">Submit</v-btn>
            </v-form>
            <div v-if="comment">{{ comment }}</div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      comment:''
    }
  },
  methods: {
    submitReservation () {
      // Add your review submission logic here
      console.log("Review submitted!");
    }
  }
}
</script>

<style>

</style>

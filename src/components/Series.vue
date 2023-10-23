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
              <v-text-field v-model="name" label="Username" required></v-text-field>
              <v-date-picker v-model="date" label="Review Date" required></v-date-picker>
              <v-textarea v-model="specialRequests" label="comment"></v-textarea>
              <v-btn color="primary" type="submit">Submit</v-btn>
            </v-form>
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
      name: "",
      email: "",
      date: new Date(),
      time: new Date(),
      partySize: 1,
      specialRequests: "",
    };
  },
  methods: {
    submitReservation () {
      // Add your review submission logic here
      console.log("Review submitted!");
    },
  },
};
</script>

<style>

</style>

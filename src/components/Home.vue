<template>
  <v-container class="ma-5">
    <v-row>
      <v-col
        v-for="(series, index) in series"
        :key="index"
        cols="12"
        sm="6"
        md="4"
      >
        <v-card>
          <!-- Series Image -->
          <v-carousel class="max-height-carousel">
            <v-carousel-item
              v-for="item in series.items"
              :key="item.name">
            <v-img :src="item.imageUrl"
              max-height="350px"></v-img>
            </v-carousel-item>
          </v-carousel>
          <v-card-title class="headline">
            {{ series.name }}
          </v-card-title>
          <v-card-text>
            {{ series.description }}
          </v-card-text>

          <v-card-actions >

            <v-btn color="blue" href="/series" >comment</v-btn>

          </v-card-actions>

        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      series: [
        {
          name: "Legend Of Fei",
          imageUrl: require("@/assets/2.jpg"),
          description: "Description for Series 1",
        },
        {
          name: "Till THe End Of The Moon",
          imageUrl: require("@/assets/2.jpg"),
          description: "Description for series 2",
        },
        {
          name: "Immortal Samsara",
          imageUrl: require("@/assets/2.jpg"),
          description: "Description for Series 3",
        },
        {
          name: "Hidden Love",
          imageUrl: require("@/assets/2.jpg"),
          description: "Description for Series 4",
        },
        {
          name: "Gen Z",
          imageUrl: require("@/assets/2.jpg"),
          description: "Description for Series 5",
        },

        {
          name: "Princess Agents",
          imageUrl: require("@/assets/2.jpg"),
          description: "Description for Series 6",
        },
        // Add more series as needed
      ],
    };
  },
};

</script>

<style>

.max-height-carousel {
  max-height: 350px; /* Adjust the max-height as needed */
}

</style>

<script setup>
import MyBar from './components/MyBar.vue'
import MyCard from './components/MyCard.vue'

</script>

<template>
  <div>
  <header>
    <MyBar />
  </header>

  <main>
    <h1 style="padding-left: 10px">Review</h1>
    <div className="gird-container">
      <MyCard />
      <MyCard />
      <MyCard />
      <MyCard />
    </div>
    </main>
  </div>
</template>

<script>
export default ({
  data () {
    return {
      item: []
    }
  },

  created () {
    .then((result) => {
      this.items = result
    })
    
  }
})
</script>


<style scoped>
.grid-container {
  display: grid;
  grid-column-gap: 0.5rem;
  grid-row-gap: 0.5rem;
}
@media (min-width: 576px) {
  .grid-container { grid-template-columns: repeat(1, 1fr); }
}
@media (min-width: 992px) {
  .grid-container { grid-template-columns: repeat(3, 1fr); }
}
</style>

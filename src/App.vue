<template>
  <div id="app">
    <span class="add-link" v-if="addNewRestaurant === false" @click="addNewRestaurant = true">Add a restaurant</span>
    <new-restaurant v-if="addNewRestaurant" @added="addRestaurant" @cancel="addNewRestaurant = false" />
    <restaurant-card v-for="restaurant in restaurants" :key="restaurant.name" :restaurant="restaurant" @removed="removeRestaurant" />
  </div>
</template>

<script>
import RestaurantCard from './components/RestaurantCard.vue'
import NewRestaurant from './components/NewRestaurant.vue'

export default {
  name: 'app',
  components: {
    RestaurantCard,
    NewRestaurant
  },
  data() {
    return {
      restaurants: [],
      addNewRestaurant: false
    }
  },
  methods: {
    addRestaurant(restaurant) {
      this.restaurants.push(restaurant)
      this.addNewRestaurant = false
    },
    removeRestaurant(removedRestaurant) {
      this.restaurants = this.restaurants.filter(restaurant => restaurant.name !== removedRestaurant.name)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.add-link {
  cursor: pointer;
}
</style>

<template>
  <div class="board">
    <lane v-for="lane in lanes" 
          :key="lane"
          :name="lane"
          :restaurants="restaurantsForLane(lane)"
          @added="addRestaurant"
          @removed="removeRestaurant" />
  </div>
</template>

<script>
import Lane from '@/components/Lane.vue'
import { lanes } from '@/constants/lanes.js'
import axios from 'axios'

const base_url = 'https://jgj-restaurants-api.herokuapp.com/restaurants'
// const base_url = 'http://localhost:8000/restaurants'
/* eslint-disable no-console */

export default {
  name: 'Board',
  components: {
    Lane
  },
  data() {
    return {
      lanes: lanes,
      restaurants: []
    }
  },
  async created() {
    const restaurantResponse = await axios.get(base_url)
    this.restaurants = restaurantResponse.data
  },
  methods: {
    restaurantsForLane(lane) {
      return this.restaurants.filter(restaurant => restaurant.lane === lane)
    },
    async addRestaurant(restaurant) {
      console.log(restaurant)
      await axios.post(base_url, restaurant)
      this.restaurants.push(restaurant)
    },
    async removeRestaurant(removedRestaurant) {
      await axios.delete(`${base_url}/${removedRestaurant._id}`)
      this.restaurants = this.restaurants.filter(restaurant => restaurant.name !== removedRestaurant.name)
    }
  }
}
</script>

<style>
.board {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: stretch;
  height: calc(100vh - 70px);
}
</style>

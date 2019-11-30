<template>
  <div class="board">
    <lane v-for="lane in lanes" 
          :key="lane"
          :name="lane"
          :restaurants="restaurantsForLane(lane)"
          @new="newRestaurant"
          @deleted="deleteRestaurant"
          @added="updateRestaurant"
          @removed="handleRemovedRestaurant"
          @moved="moveRestaurant"
          @rated="rateRestaurant" />
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
      return this.restaurants.filter(restaurant => restaurant.lane === lane).sort((a, b) => {
        return a.displayOrder - b.displayOrder
      })
    },
    async newRestaurant(restaurant) {
      const newRestaurant = await axios.post(base_url, restaurant)
      this.restaurants.push(newRestaurant.data)
    },
    async deleteRestaurant(deletedRestaurant) {
      await axios.delete(`${base_url}/${deletedRestaurant._id}`)
      this.restaurants = this.restaurants.filter(restaurant => restaurant.name !== deletedRestaurant.name)
    },
    async updateRestaurant(updatedRestaurantEvent) {
      const updatedRestaurant = updatedRestaurantEvent.event.element
      const newIndex = updatedRestaurantEvent.event.newIndex

      const existingRestaurant = this.restaurants.find(restaurant => restaurant._id === updatedRestaurant._id)
      
      const restaurantsInLane = this.restaurantsForLane(updatedRestaurantEvent.lane)
      restaurantsInLane.splice(newIndex, 0, existingRestaurant)
      existingRestaurant.lane = updatedRestaurantEvent.lane
      
      await this.updateDisplayOrder(restaurantsInLane)
    },
    async moveRestaurant(movedRestaurantEvent) {
      const movedRestaurant = movedRestaurantEvent.element
      const newIndex = movedRestaurantEvent.newIndex
      const oldIndex = movedRestaurantEvent.oldIndex
      
      const restaurantsInLane = this.restaurantsForLane(movedRestaurant.lane)
      restaurantsInLane.splice(oldIndex, 1)
      restaurantsInLane.splice(newIndex, 0, movedRestaurant)
      
      await this.updateDisplayOrder(restaurantsInLane)
    },
    async handleRemovedRestaurant(removedRestaurantEvent) {
      const restaurantsInLane = this.restaurantsForLane(removedRestaurantEvent.lane)
      await this.updateDisplayOrder(restaurantsInLane)
    },
    async updateDisplayOrder(restaurantsInLane) {
      let restaurantUpdates = []
      restaurantsInLane.forEach(restaurant => {
        restaurant.displayOrder = restaurantsInLane.indexOf(restaurant)
        restaurantUpdates.push(axios.put(`${base_url}/${restaurant._id}`, restaurant))
      })

      await Promise.all(restaurantUpdates)
    },
    async rateRestaurant(ratedRestaurantEvent) {
      const ratedRestaurant = ratedRestaurantEvent.restaurant
      const existingRestaurant = this.restaurants.find(restaurant => restaurant._id === ratedRestaurant._id)
      existingRestaurant.userRating = ratedRestaurantEvent.userRating
      await axios.put(`${base_url}/${existingRestaurant._id}`, existingRestaurant)
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
  height: calc(100vh - 60px);
}
</style>

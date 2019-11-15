<template>
  <div class="board">
    <!-- <span class="add-link" v-if="addNewRestaurant === false" @click="addNewRestaurant = true">Add a restaurant</span> -->
    <lane />
    <!-- <new-restaurant v-if="addNewRestaurant" @added="addRestaurant" @cancel="addNewRestaurant = false" />
    <restaurant-card v-for="restaurant in restaurants" :key="restaurant.name" :restaurant="restaurant" @removed="removeRestaurant" /> -->
  </div>
</template>

<script>
// import RestaurantCard from '@/components/RestaurantCard.vue'
// import NewRestaurant from '@/components/NewRestaurant.vue'
import Lane from '@/components/Lane.vue'

export default {
  name: 'Board',
  components: {
    // RestaurantCard,
    // NewRestaurant,
    Lane
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
.board {
  display: flex;
  flex-direction: row;
  align-items: stretch;
}

.add-link {
  cursor: pointer;
}
</style>

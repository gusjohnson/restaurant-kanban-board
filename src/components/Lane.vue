<template>
  <div class="lane">
    <h1>{{ name }}</h1>
    <span class="add-link" v-if="addNewRestaurant === false" @click="addNewRestaurant = true">Add a restaurant</span>
    <new-restaurant v-if="addNewRestaurant" @added="addRestaurant" @cancel="addNewRestaurant = false" />
    <restaurant-card v-for="restaurant in restaurants" :key="restaurant.name" :restaurant="restaurant" @removed="removeRestaurant" />
  </div>
</template>

<script>
import RestaurantCard from '@/components/RestaurantCard.vue'
import NewRestaurant from '@/components/NewRestaurant.vue'

export default {
  name: 'Lane',
  components: {
    RestaurantCard,
    NewRestaurant
  },
  props: {
    name: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      restaurants: [],
      addNewRestaurant: false,
    }
  },
  methods: {
    addRestaurant(restaurant) {
      this.restaurants.push({
        ...restaurant,
        lane: this.name,
        displayOrder: this.restaurants.length
      })
      this.addNewRestaurant = false
    },
    removeRestaurant(removedRestaurant) {
      this.restaurants = this.restaurants.filter(restaurant => restaurant.name !== removedRestaurant.name)
    }
  }
}
</script>

<style scoped>
.lane {
  width: 20rem;
  height: 100%;
  border: 1px solid gray;
  border-radius: 0.5rem;
}

.add-link {
  cursor: pointer;
}
</style>
<template>
  <div class="lane">
    <h1>{{ name }}</h1>
    <span class="add-link" v-if="addNewRestaurant === false" @click="addNewRestaurant = true">Add a restaurant</span>
    <new-restaurant v-if="addNewRestaurant" @added="addRestaurant" @cancel="addNewRestaurant = false" />
    <draggable class="dropzone" :list="restaurants" group="restaurants">
      <restaurant-card v-for="restaurant in restaurants" :key="restaurant.name" :restaurant="restaurant" @removed="removeRestaurant" />
    </draggable>
  </div>
</template>

<script>
import RestaurantCard from '@/components/RestaurantCard.vue'
import NewRestaurant from '@/components/NewRestaurant.vue'
import draggable from 'vuedraggable'

export default {
  name: 'Lane',
  components: {
    RestaurantCard,
    NewRestaurant,
    draggable
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

<style lang="scss" scoped>
.lane {
  width: 20rem;
  height: 100%;
  border: 1px solid gray;
  border-radius: 0.5rem;
  display: flex;
  flex-direction: column;
  overflow: scroll;

  .dropzone {
    height: 100%;
  }
}

.add-link {
  cursor: pointer;
}
</style>
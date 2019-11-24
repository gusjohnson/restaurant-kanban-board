<template>
  <div class="lane">
    <h1>{{ name }}</h1>
    <span class="add-link" v-if="addNewRestaurant === false" @click="addNewRestaurant = true">Add a restaurant</span>
    <new-restaurant v-if="addNewRestaurant" @added="addRestaurant" @cancel="addNewRestaurant = false" />
    <draggable class="dropzone" :list="restaurants" group="restaurants" @change="updateRestaurant">
      <restaurant-card v-for="restaurant in restaurants" :key="restaurant.name" :restaurant="restaurant" @removed="removeRestaurant" />
    </draggable>
  </div>
</template>

<script>
import RestaurantCard from '@/components/RestaurantCard.vue'
import NewRestaurant from '@/components/NewRestaurant.vue'
import draggable from 'vuedraggable'
import _has from 'lodash/has'

/* eslint-disable no-console */

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
    },
    restaurants: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      addNewRestaurant: false
    }
  },
  methods: {
    addRestaurant(restaurant) {
      this.$emit('new', {
        ...restaurant,
        userRating: null,
        lane: this.name
      })
      this.addNewRestaurant = false
    },
    removeRestaurant(removedRestaurant) {
      this.$emit('removed', removedRestaurant)
    },
    updateRestaurant(event) {
      if (_has(event, 'added')) {
        event.added.element.lane = this.name
        this.$emit('added', event.added)
      } else if (_has(event, 'moved')) {
        this.$emit('moved', event.moved)
      }
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
<template>
  <div class="lane">
    <h1>{{ name }}</h1>
    <span class="add-link" v-if="addNewRestaurant === false" @click="addNewRestaurant = true">Add a restaurant</span>
    <new-restaurant v-if="addNewRestaurant" @added="addRestaurant" @cancel="addNewRestaurant = false" />
    <draggable class="dropzone" :list="restaurants" group="restaurants" @change="updateRestaurant">
      <restaurant-card v-for="restaurant in restaurants" :key="restaurant.name" :restaurant="restaurant" @deleted="deleteRestaurant" />
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
        lane: this.name,
        displayOrder: this.restaurants.length
      })
      this.addNewRestaurant = false
    },
    deleteRestaurant(deletedRestaurant) {
      this.$emit('deleted', deletedRestaurant)
    },
    updateRestaurant(event) {
      if (_has(event, 'added')) {
        this.$emit('added', {
            event: event.added,
            lane: this.name
          })
      } else if (_has(event, 'moved')) {
        this.$emit('moved', event.moved)
      } else if (_has(event, 'removed')) {
        this.$emit('removed', {
            event: event.removed,
            lane: this.name
          })
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.lane {
  width: 20rem;
  height: 100%;
  border-right: 1px solid rgb(189, 189, 189);
  display: flex;
  flex-direction: column;
  background-color: #f7f7f7;

  .dropzone {
    height: 100%;
    overflow: scroll;
  }
}

.add-link {
  cursor: pointer;
}
</style>
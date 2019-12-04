<template>
  <div class="card">
    <div class="name-and-rating">
      <span class="name">{{ restaurant.name }}</span>
      <font-awesome-icon icon="trash-alt" class="remove-restaurant" @click="$emit('deleted', restaurant)" />
    </div>
    <div class="address">{{ restaurant.address }}</div>
    <div class="rating"><b>Google Rating:</b> {{ restaurant.googleRating }}
      <font-awesome-icon icon="star" style="color: #f0ad4e" />
    </div>
    <div class="rating"><b>Your Rating:</b>
      <span v-if="restaurant.userRating"> {{ restaurant.userRating }}
        <font-awesome-icon icon="star" style="color: #f0ad4e" />
      </span>
      <span v-else>
        <font-awesome-icon v-if="!addRating" icon="plus-circle" class="user-rating-button" @click="addRating = true" />
        <input v-if="addRating" v-model="userRating" class="rating-input" type="number" max=5 min=0 />
        <font-awesome-icon v-if="addRating" icon="save" class="user-rating-button" @click="saveRating" />
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RestaurantCard',
  props: {
    restaurant: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      addRating: false,
      userRating: null
    }
  },
  methods: {
    saveRating() {
      this.$emit('rated', {
        restaurant: this.restaurant,
        userRating: this.userRating
      })
      this.userRating = null
      this.addRating = false
    }
  }
}
</script>

<style scoped>
.card {
  height: 9rem;
  border: 1px solid gray;
  border-radius: 0.25rem;
  margin: 1rem;
  box-shadow: 2px 2px 4px gray;
  font-size: 14px;
  text-align: left;
  cursor: move;
}

.card > div {
  text-align: left;
  padding: .5rem .5rem 0 .5rem;
}

.name-and-rating {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

.name {
  flex-basis: 95%;
  font-weight: bold;
  font-size: 15px;
}

.remove-restaurant {
  cursor: pointer;
  color: #d9534f;
}

.user-rating-button {
  color: #5cb85c;
  padding-left: .25rem;
  cursor: pointer;
}

.icon {
  padding-left: .25rem;
}

.rating-input {
  width: 2rem;
  margin-left: .25rem;
}
</style>
<template>
  <div class="card">
    <span class="remove-restaurant" @click="$emit('deleted', restaurant)">Remove</span>
    <div>{{ restaurant.name }}</div>
    <div>{{ restaurant.rating }}</div>
    <div>{{ restaurant.address }}</div>
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
  }
}
</script>

<style scoped>
.card {
  height: 10rem;
  border: 1px solid gray;
  border-radius: 0.25rem;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  margin: 1rem;
  box-shadow: 1px 1px 5px gray;
}

.remove-restaurant {
  align-self: flex-start;
  padding-left: .5rem;
  cursor: pointer;
}
</style>
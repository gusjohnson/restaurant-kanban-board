<template>
  <div class="card">
    <span class="cancel" @click="$emit('cancel')">Cancel</span>
    <input ref="autocomplete" 
        placeholder="Search" 
        class="search-box"
        onfocus="value = ''" 
        type="text" />
  </div>
</template>

<script>
/* eslint-disable no-undef */

export default {
  name: 'NewRestaurant',
  data() {
    return {
      autocomplete: null
    }
  },
  mounted() {
    this.autocomplete = new google.maps.places.Autocomplete(this.$refs.autocomplete, { types: ['establishment'] })
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(function(position) {
        var geolocation = {
          lat: position.coords.latitude,
          lng: position.coords.longitude
        }
        var circle = new google.maps.Circle({center: geolocation, radius: position.coords.accuracy})
        this.autocomplete.setBounds(circle.getBounds())
      })
    }
    this.autocomplete.addListener('place_changed', this.placeSelected)
  },
  methods: {
    placeSelected() {
      const place = this.autocomplete.getPlace()
      if (place) {
        this.$emit('added', {
          name: place.name,
          googleRating: place.rating,
          address: place.formatted_address
        })
      }
    }
  }
}
</script>

<style scoped>
.card {
  height: 9rem;
  border: 1px solid gray;
  border-radius: 0.25rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  margin: 1rem;
  box-shadow: 2px 2px 4px gray;
  font-size: 14px;
  background-color: #e9e9e9;
}

.search-box {
  height: 1.5rem;
  width: 75%;
  cursor: text;
}

.cancel {
  align-self: flex-start;
  padding: .5rem;
  cursor: pointer;
}
</style>
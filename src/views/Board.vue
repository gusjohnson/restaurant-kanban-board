<template>
  <div class="board">
    <lane v-for="lane in lanes" :key="lane" :name="lane" />
  </div>
</template>

<script>
import Lane from '@/components/Lane.vue'
import { lanes } from '@/constants/lanes.js'

export default {
  name: 'Board',
  components: {
    Lane
  },
  data() {
    return {
      lanes: lanes
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

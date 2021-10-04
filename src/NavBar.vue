<template>
  <div class="nav-bar">
    <h2 class="link">Restaurant Prioritizer</h2>
  </div>
</template>

<script>
export default {
  name: 'NavBar'
}
</script>

<style scoped>
.nav-bar {
  width: 100%;
  height: 60px;
  background-color: #1c526b;
  display: flex;
  align-items: center;
}

.link {
  padding-left: 1rem;
  padding-right: 1rem;
  color: #f7f7f7;
}
</style>
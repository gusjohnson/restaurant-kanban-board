<template>
  <div class="nav-bar">
    <h2 class="link">Restaurant Kanban Board</h2>
    <span class="link">Home</span>
    <span class="link">Random</span>
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
  background-color: #292b2c;
  display: flex;
  align-items: center;
}

.link {
  padding-left: 1rem;
  padding-right: 1rem;
  color: #f7f7f7;
}
</style>
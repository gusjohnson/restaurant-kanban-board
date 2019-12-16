<template>
  <div class="modal-background">
    <div class="modal-content">
      <h1>Login fool</h1>
      <div class="modal-fields">
        <div class="modal-row">
          <label>E-mail: </label>
          <input type="email" />
        </div>
        <div class="modal-row">
          <label>Password: </label>
          <input type="password" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'LoginModal',
  data() {
    return {
      user: {}
    }
  }
}
</script>

<style>
.modal-background {
  height: 100%;
  width: 100%;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.7); /* Black w/ opacity */
}

.modal-content {
  height: 50%;
  width: 35%;
  /* background-color: #f7f7f7; */
  margin: 15% auto;
  padding: 20px;
  color: #fefefe;
}

.modal-fields {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.modal-row {
  width: 75%;
  display: flex;
  justify-content: flex-end;
  padding: .5em;
}

.modal-row > label {
  padding: .25em 1em .25em 0;
  flex: 1;
}
.modal-row > input {
  flex: 2;
}
</style>

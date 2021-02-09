<template>
  <button class="c-button" @click="$emit('onKeyPressed', label)">{{ label }}</button>
</template>

<script>
export default {
  name: "c-button",
  props: {
    label: {
      type: String
    }
  }
}
</script>

<style scoped>
.c-button {
  height: 10vh;
  width: 10vh;
  margin: 1px;

  background-color: #c1dee7;
  border: none;

  color: #184766;
  font-family: pock, sans-serif;
  font-size: 4vh;

  border-radius: 0.2em;
}

.c-button:hover {
  background-color: #237b90;
  box-shadow: 0 0 15px #f891a0;
}

.c-button:active {
  background-color: #f891a0;
}

.c-button:focus {
  outline: none;
  box-shadow: none;
}
</style>
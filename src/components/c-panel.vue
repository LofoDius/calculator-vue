<template>
  <div class="c-panel__container">
    {{value}}
  </div>
</template>

<script>
export default {
  name: "c-panel",

  props: {
    value: {
      type: String,
      default: "123"
    }
  }
}
</script>

<style scoped>
.c-panel__container {
  display: flex;
  border: #237b90 2px solid;
  background-color: #f2f7fc;
  height: 10vh;
  width: 100%;
  margin-bottom: 50px;
}
</style>
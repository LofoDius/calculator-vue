<template>
  <div class="c-panel__container">
    <div class="c-panel__memory-value" v-if="memoryValue != 0">
      Memory: {{ memoryValue }}
    </div>
    <div class="c-panel__value">
      {{ value }}
    </div>
  </div>
</template>

<script>
export default {
  name: "c-panel",

  props: {
    value: {
      type: String,
      default: ""
    },
    memoryValue: {
      type: String,
      default: ""
    }
  }
}
</script>

<style scoped>
.c-panel__container {
  position: relative;

  border: rgba(35, 125, 144, 0.5) 2px solid;
  background-color: #f2f7fc;
  width: 100%;
  margin-bottom: 50px;
}

.c-panel__value {
  font-family: pock, sans-serif;
  display: flex;
  height: 10vh;
  justify-content: flex-end;
  align-items: center;
  font-size: 8vh;
  padding-right: 5px;
  color: #225485;
}

.c-panel__memory-value {
  position: absolute;
  margin-left: 3px;
  color: #b83b48;
}
</style>
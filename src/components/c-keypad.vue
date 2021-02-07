<template>
  <div class="c-keypad__container">
    <c-button v-for="key in keys" :key="key" :label="key"/>
  </div>
</template>

<script>
import cButton from '@/components/c-button'
export default {
  name: "c-keypad",
  components: {
    cButton
  },
  data() {
    return {
      keys: ['7', '8', '9', '4', '5', '6', '1', '2', '3', '0', '.']
    }
  }
}
</script>

<style scoped>
.c-keypad__container {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-content: center;

  max-width: calc(30vh + 6px);
  width: 60%;
}

.c-button:nth-child(10) {
  width: calc(20vh + 2px);
}
</style>
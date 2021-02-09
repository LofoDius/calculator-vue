<template>
  <div class="c-memory-functions-container">
    <c-button v-for="fun in functions" :key="fun" :label="fun" @onKeyPressed="onKeyPressed"/>
  </div>
</template>

<script>
import CButton from "@/components/c-button";

export default {
  name: "c-memory-functions",
  components: {CButton},
  data() {
    return {
      functions: ['MS', 'MR', 'M+']
    }
  },

  methods: {
    onKeyPressed(label) {
      this.$emit('onKeyPressed', label);
    }
  }
}
</script>

<style scoped>
.c-memory-functions-container {
  display: flex;
}

.c-memory-functions-container .c-button {
  font-size: 3.5vh;
  letter-spacing: 2px;
}
</style>
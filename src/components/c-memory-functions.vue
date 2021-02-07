<template>
  <div class="c-memory-functions-container">
    <c-button v-for="fun in functions" :key="fun" :label="fun"/>
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
  }
}
</script>

<style scoped>
.c-memory-functions-container {
  display: flex;
}
</style>
<template>
  <div class="c-operations__container">
    <c-button v-for="operation in operations" :key="operation" :label="operation"/>
  </div>
</template>

<script>
import cButton from '@/components/c-button'
export default {
  name: "c-operations",
  components: {
    cButton
  },
  data() {
    return {
      operations: ['+', '×', '−', '÷']
    }
  }
}
</script>

<style scoped>
.c-operations__container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: flex-start;
  height: calc(20vh + 4px);
  margin-top: 10px;
}
</style>
<template>
  <div class="c-modifiers__container">
    <c-button label="±"/>
    <c-button label="e"/>
  </div>
</template>

<script>
import cButton from '@/components/c-button'
export default {
  name: "c-modifiers",
  components: {
    cButton
  }
}
</script>

<style scoped>
.c-modifiers__container {
  display: flex;
}
</style>
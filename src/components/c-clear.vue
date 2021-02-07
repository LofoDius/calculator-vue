<template>
  <div class="c-clear__container">
<!--    TODO добавить хинты-->
    <c-button label="CA" @onKeyPressed="$emit('onKeyPressed', 'CA')"/>
    <c-button label="⌫" @onKeyPressed="$emit('onKeyPressed', '⌫')"/>
  </div>
</template>

<script>
import cButton from '@/components/c-button'
export default {
  name: "c-clear",
  components: {
    cButton
  }
}
</script>

<style scoped>
.c-clear__container {
  display: flex;
  justify-content: flex-end;

  width: 100%;

  margin-bottom: 10px;
}
</style>
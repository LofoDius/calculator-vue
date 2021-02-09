<template>
  <div class="c-modifiers__container">
    <c-button label="e" @onKeyPressed="$emit('onKeyPressed', 'e')"/>
    <c-button label="/" @onKeyPressed="$emit('onKeyPressed', '+/-')"/>
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

.c-button:last-child {
  letter-spacing: -1px;
  vertical-align: bottom;
}

.c-button:last-child:before {
  content: '+';
  vertical-align: 5px;
}

.c-button:last-child:after {
  content: '-';
  vertical-align: sub;

}

</style>
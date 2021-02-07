<template>
  <div class="c-operations__container">
    <c-button
        v-for="operation in operations"
        :key="operation"
        :label="operation"
        @onKeyPressed="onKeyPressed"
        :class="isActive === operation ? 'active' : ''"
    />
  </div>
</template>

<script>
import cButton from '@/components/c-button'

export default {
  name: "c-operations",
  components: {
    cButton
  },

  props: {
    highlight: {
      type: String,
      default: ''
    }
  },

  data() {
    return {
      operations: ['+', '×', '-', '÷']
    }
  },

  computed: {
    isActive() {
      return this.highlight;
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
.c-operations__container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: flex-start;
  height: calc(20vh + 4px);
  margin-top: 10px;
}

.active {
  background-color: lightpink;
}
</style>
<template>
  <div class="c-calc__container">
    <c-panel/>
    <div class="c-calc__memory">
      <c-memory-functions/>
      <c-clear/>
    </div>
    <div class="temp">
      <c-keypad/>
      <div class="right">
        <c-modifiers/>
        <c-operations/>
        <c-button label="="/>
      </div>
    </div>
  </div>
</template>

<script>
import cPanel from '@/components/c-panel'
import cClear from '@/components/c-clear'
import cKeypad from '@/components/c-keypad'
import cModifiers from '@/components/c-modifiers'
import cOperations from '@/components/c-operations'
import cButton from '@/components/c-button'
import cMemoryFunctions from '@/components/c-memory-functions'

export default {
  name: "c-calc",
  components: {
    cPanel,
    cClear,
    cKeypad,
    cModifiers,
    cOperations,
    cButton,
    cMemoryFunctions
  }
}
</script>

<style scoped>
/*TODO поменять минимальные*/
.c-calc__container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;

  min-height: 450px;
  min-width: 350px;
  height: 75vh;
  width: 60vh;

  padding: 20px;

  background-color: #f8f8f5;
  border: #f891a0 2px solid;
  border-radius: 7px;
}

.temp {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 100%;
}

.c-keypad__container {
  height: calc(40vh + 10px);
}

.right {
  display: flex;
  flex-flow: column wrap;
  height: calc(40vh + 10px);
}

.c-button:last-child {
  margin-top: 10px;
  width: calc(20vh + 2px);
  height: calc(10vh - 17px);
  align-self: flex-start;
}

.c-calc__memory {
  display: flex;

}

.c-button:last-child {
  background-color: #f891a0;
}

.c-button:last-child:hover {
  box-shadow: 0 0 20px #237b90;
  border: 2px #f891a0 solid;
  border-radius: 0.2em;
}
</style>
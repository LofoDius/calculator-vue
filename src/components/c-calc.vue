<template>
  <div class="c-calc__container">
    <c-panel :value="displayText" :memory-value="memoryValue"/>
    <div class="c-calc__memory">
      <c-memory-functions @onKeyPressed="onKeyPressed"/>
      <c-clear @onKeyPressed="onKeyPressed"/>
    </div>
    <div class="temp">
      <c-keypad @onKeyPressed="onKeyPressed"/>
      <div class="right">
        <c-modifiers @onKeyPressed="onKeyPressed"/>
        <c-operations @onKeyPressed="onKeyPressed" :highlight="highlightAction"/>
        <c-button label="=" @onKeyPressed="compute"/>
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
  },

  data() {
    return {
      display: '0',
      numberKeys: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0'],
      operationKeys: ['+', '×', '-', '÷'],
      currentAction: '',
      lastValue: 0,
      inMemoryValue: 0,
      isResultVisible: false,
      isPrevNumberVisible: false
    }
  },

  computed: {
    displayText() {
      return this.display;
    },

    memoryValue() {
      return this.inMemoryValue.toString();
    },

    highlightAction() {
      return this.currentAction;
    }
  },

  methods: {
    onKeyPressed(label) {
      switch (label) {
        case '.': {
          if (this.display.includes('.') || this.display.includes('e')) break;
          else this.display += '.';
          break;
        }
        case '⌫': {
          if (this.display === '0') break;
          this.display = this.display.substring(0, this.display.length - 1);
          if (this.display.length === 0) this.display = '0';
          break;
        }
        case 'CA': {
          this.display = '0';
          this.currentAction = '';
          this.lastValue = 0;
          break;
        }
        case 'e': {
          if (this.display.includes('e')) {
            this.display = this.display.split('e')[0]
            break;
          }

          if (this.isResultVisible) {
            this.currentAction = '';
            this.lastValue = 0;
            this.isResultVisible = false;
          }

          this.display += 'e+';
          break;
        }
        case '±': {
          if (this.display === '0') break;
          if (this.display[0] === '-') this.display = this.display.substring(1, this.display.length);
          else this.display = '-' + this.display;
          break;
        }
        case 'MS': {
          this.inMemoryValue = parseFloat(this.display);
          this.isResultVisible = true;
          break;
        }
        case 'MR': {
          if (this.inMemoryValue === null) break;

          if (this.currentAction !== '') {
            this.lastValue = parseFloat(this.display);
            this.display = this.inMemoryValue.toString();
            this.compute();
            return;
          }

          this.display = this.inMemoryValue.toString();
          break;
        }
        case 'M+': {
          if (this.inMemoryValue === null) this.inMemoryValue = 0;

          this.inMemoryValue += parseFloat(this.display);
          this.isResultVisible = true;
          break;
        }
        default: {
          if (this.operationKeys.includes(label)) {
            this.operationHandler(label);
          } else if (this.numberKeys.includes(label)) {
            this.numberHandler(label);
          }
        }
      }
    },

    operationHandler(label) {
      if (this.display[this.display.length - 2] === 'e' && label === '-') {
        this.display = this.display.replace('+', '-');
        return;
      }

      if (this.display[this.display.length - 2] === 'e' && label === '+') {
        this.display = this.display.replace('-', '+');
        return;
      }

      if (this.currentAction !== '') {
        this.compute();
      }

      this.isPrevNumberVisible = true;
      this.isResultVisible = false;
      this.lastValue = parseFloat(this.display);
      this.currentAction = label;
    },

    numberHandler(label) {
      if (this.isPrevNumberVisible) {
        this.display = label;
        this.isPrevNumberVisible = false;
        return;
      }

      if (this.isResultVisible) {
        this.display = label;
        this.lastValue = 0;
        this.currentAction = '';
        this.isResultVisible = false;
        return;
      }

      if (this.display === '0') {
        if (label === '0') return;
        else {
          this.display = label;
          return;
        }
      }

      if (this.display.includes('e')) {
        let lengthCheck = this.display.split('e');
        if (lengthCheck[1].length >= 4) {
          return
        }
      } else if (this.display.length >= 8)
        return;

      this.display += label;
    },

    compute() {
      switch (this.currentAction) {
        case '-': {
          this.display = (this.lastValue - parseFloat(this.display)).toString();
          this.lastValue = parseFloat(this.display);
          this.isResultVisible = true;
          break;
        }
        case '+': {
          this.display = (this.lastValue + parseFloat(this.display)).toString();
          break;
        }
        case '×': {
          this.display = (this.lastValue * parseFloat(this.display)).toString();
          break;
        }
        case '÷': {
          if (parseFloat(this.display) === 0) {
            this.display = '0';
            this.lastValue = 0;
            this.currentAction = '';
            this.$notify({type: 'error', text: 'Error: division by zero!'});
            break;
          }
          this.display = (this.lastValue / parseFloat(this.display)).toString();
          break;
        }
      }
      if (this.display.length > 8) {
        this.display = (parseFloat(this.display)).toExponential(6);
      }
      this.currentAction = '';
      this.lastValue = parseFloat(this.display);
      this.isResultVisible = true;
    }
  }
}
</script>

<style scoped>
.c-calc__container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;

  height: calc(75vh + (120px - 12vh));
  width: calc(60vh + (50px - 3vh));

  padding: 20px;

  background-color: #f8f8f5;
  border: #f891a0 2px solid;
  border-radius: 7px;
  box-shadow: 10px 15px 4px rgba(196,178,209, 0.35);
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
  color: #b83b48;
}

.c-button:last-child:hover {
  box-shadow: 0 0 20px #fa6e6e;
  border-radius: 0.2em;
  color: #bb414f;
}

.c-button:last-child:active {
  background-color: #ef6773;
}
</style>
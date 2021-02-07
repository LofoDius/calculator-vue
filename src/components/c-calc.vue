<template>
  <div class="c-calc__container">
    <c-panel :value="displayText"/>
    <div class="c-calc__memory">
      <c-memory-functions @onKeyPressed="onKeyPressed"/>
      <c-clear @onKeyPressed="onKeyPressed"/>
    </div>
    <div class="temp">
      <c-keypad @onKeyPressed="onKeyPressed"/>
      <div class="right">
        <c-modifiers @onKeyPressed="onKeyPressed"/>
        <c-operations @onKeyPressed="onKeyPressed"/>
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
      inMemoryValue: null,
      isResultVisible: false
    }
  },

  computed: {
    displayText() {
      return this.display;
    }
  },

  methods: {
    onKeyPressed(label) {
      switch (label) {
        case '.': {
          if (this.display.includes(',')) break;
          else this.display += '.';
          break;
        }
        case '⌫': {
          if (this.display === '0') break;
          this.display = this.display.substring(0, this.display.length - 1);
          break;
        }
        case 'CA': {
          this.display = '0';
          this.currentAction = '';
          this.lastValue = 0;
          this.inMemoryValue = null;
          break;
        }
        case 'e': {
          if (this.display === '') this.display = '0';

          if (this.isResultVisible) {
            this.currentAction = '';
            this.lastValue = 0;
          }

          this.display += 'e';
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
            this.display = this.inMemoryValue.toString();
            this.compute();
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
      if (this.display[this.display.length - 1] === 'e' && label === '-') {
        this.display += '-';
        return;
      }

      console.log(parseFloat(this.display));
      this.lastValue = parseFloat(this.display);
      this.display = '0';
      this.currentAction = label;
    },

    numberHandler(label) {
      if (this.isResultVisible) {
        this.display = label;
        this.lastValue = 0;
        this.currentAction = ''
      }

      if (this.display === '0') {
        if (label === '0') return;
        else {
          this.display = label;
          return;
        }
      }

      this.display += label;
    },

    compute() {
      console.log('currentAction: ', this.currentAction);
      console.log('lastValue: ', this.lastValue);
      console.log('display: ', parseFloat(this.display));

      switch (this.currentAction) {
        case '-': {
          this.display = (this.lastValue - parseFloat(this.display)).toString();
          this.lastValue = parseFloat(this.display);
          break;
        }
        case '+': {
          this.display = (this.lastValue + parseFloat(this.display)).toString();
          this.lastValue = parseFloat(this.display);
          break;
        }
        case '×': {
          this.display = (this.lastValue * parseFloat(this.display)).toString();
          this.lastValue = parseFloat(this.display);
          break;
        }
        case '÷': {
          if (parseFloat(this.display) === 0) {
            this.display = '0';
            this.lastValue = 0;
            this.inMemoryValue = null;
            this.currentAction = '';
            alert('Error: division by zero!');
            break;
          }
          this.display = (this.lastValue / parseFloat(this.display)).toString();
          this.lastValue = parseFloat(this.display);
          break;
        }
      }
    }
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
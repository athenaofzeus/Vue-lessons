<template>
  <div class="container">
    <div class="calc-corpus">
      <div class="operands">
        <div>
          <input type="radio" id="first" value="operand1" v-model="piked">
          <input v-model.number="operand1" type="number">
        </div>
        <div>
          <input type="radio" id="second" value="operand2" v-model="piked">
          <input v-model.number="operand2" type="number">
        </div>
        <div class="result" v-if="!error">{{ result }} <br>Fib ={{ fibResult }}</div>
        <div class="result" v-else>Error! {{ error }}</div>
      </div>

      <div class="buttons">
        <button class="delete" @click="deleteSymbol">←</button>
        <button class="butt-operator" v-for="operator in operators" :title="operator" :key="operator" :disabled="(operand1 === '' || operand2 === '')" @click="calculation(operator)">{{operator}}</button>
      </div>
      <div class="keybord">
        <div class="num-buttons" v-show="checked">
          <button class="number" v-for="num in keybord" :key="num" value="num" @click="inputNum(num)">{{ num }}</button>
        </div>
        <input type="checkbox" id="checkbox" v-model="checked">
        <label for="checkbox">Show keybord</label>
      </div>
    </div>

    <div class="history">
      <div class="history-line" v-for="(str, id) in logs" :key="id">{{str}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FirstCalc',
  data () {
    return {
      operators: ['+', '-', '*', '/', '//', '^'],
      operand1: 0,
      operand2: 0,
      result: 0,
      error: '',
      fibResult: 0,
      logs: {},
      checked: false,
      keybord: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0],
      piked: ''
    }
  },
  methods: {
    calculation (operator) {
      this.error = ''
      switch (operator) {
        case '+':
          this.sum()
          break
        case '-':
          this.sub()
          break
        case '*':
          this.mult()
          break
        case '/':
          this.div()
          break
        case '//':
          this.divRound()
          break
        case '^':
          this.power()
          break
      }
      // this.logs[Date.now()] = `${this.operand1} ${operator} ${this.operand2} = ${this.result}`
      this.$set(this.logs, Date.now(), `${this.operand1} ${operator} ${this.operand2} = ${this.result}`)
    },
    sum () {
      this.result = this.operand1 + this.operand2
      this.fibResult = this.fib1 + this.fib2
    },
    sub () {
      this.result = this.operand1 - this.operand2
      this.fibResult = this.fib1 - this.fib2
    },
    mult () {
      this.result = this.operand1 * this.operand2
      this.fibResult = this.fib1 * this.fib2
    },
    div () {
      this.result = this.operand1 / this.operand2
      this.fibResult = this.fib1 / this.fib2
      if (this.result === Infinity) {
        this.error = 'Недопустимое значение'
      }
    },
    divRound () {
      this.result = Math.floor(this.operand1 / this.operand2)
      this.fibResult = Math.floor(this.fib1 / this.fib2)
    },
    power () {
      this.result = this.operand1 ** this.operand2
      this.fibResult = this.fib1 ** this.fib2
    },
    fib (n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2)
    },
    inputNum (value) {
      if (this.piked === 'operand1') {
        if (this.operand1 === 0) {
          this.operand1 = ''
        }
        this.operand1 = Number('' + this.operand1 + value)
      } else {
        if (this.operand2 === 0) {
          this.operand2 = ''
        }
        this.operand2 = Number('' + this.operand2 + value)
      }
    },
    deleteSymbol () {
      if (this.piked === 'operand1') {
        this.operand1 = Number(this.operand1.toString().slice(0, -1))
      } else {
        this.operand2 = Number(this.operand2.toString().slice(0, -1))
      }
    }
  },

  computed: {
    fib1 () {
      return this.fib(this.operand1)
    },
    fib2 () {
      return this.fib(this.operand2)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .container {
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-column-gap: 10%;
  }
  .calc-corpus{
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }
  .operands {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }
  .buttons {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 5px;
  }
  .delete:first-child {
    grid-column-start: 1;
    grid-column-end: 3;
    width: unset;
  }
  button {
    background-color: white;
    border: 1px solid silver;
    cursor: pointer;
    color: rgb(80, 80, 80);
    width: 30px;
    font-size: 18px;
  }
  .history {
    padding-top: 3px;
  }
  label {
    font-size: 12px;
    color: gray
  }
  .num-buttons {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 5px;
    margin-top: -24px;
  }
  .number:first-child {
    grid-column-start: 4;
  }
  .number:last-child {
    grid-column-start: 3;
    grid-column-end: 6;
    width: unset;
  }
</style>

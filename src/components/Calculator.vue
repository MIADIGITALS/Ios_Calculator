<template>
  <div class='calculator'>
    <div class="display">{{ current || '0' }}</div>
    <div @click="clear" class="button">C</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percent" class="button">%</div>
    <div @click="divide" class="button operator">/</div>
    <div @click="append('7')" class="button">7</div>
    <div @click="append('8')" class="button">8</div>
    <div @click="append('9')" class="button">9</div>
    <div @click="times" class="button operator">*</div>
    <div @click="append('4')" class="button">4</div>
    <div @click="append('5')" class="button">5</div>
    <div @click="append('6')" class="button">6</div>
    <div @click="minus" class="button operator">-</div>
    <div @click="append('1')" class="button">1</div>
    <div @click="append('2')" class="button">2</div>
    <div @click="append('3')" class="button">3</div>
    <div @click="plus" class="button operator">+</div>
    <div @click="append('0')"  class="button zero">0</div>
    <div @click="dot" class="button">.</div>
    <div @click="equal" class="button operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      operator: null,
      previous: null,
      operatorclicked: false
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current) / 10}`
    },
    append(number) {
      if (this.operatorclicked) {
        this.current = ''
        this.operatorclicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setprevious() {
      this.previous = this.current
      this.operatorclicked = true
    }, 
    divide() {
      this.operator = (a, b) => a / b
      this.setprevious()
    },
    times() {
      this.operator = (a, b) => a * b
      this.setprevious()
    },
    minus() {
      this.operator = (a, b) => b - a
      this.setprevious()
    },
    plus() {
      this.operator = (a, b) => a + b
      this.setprevious()
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`
      this.previous = null
    }

  }
}
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr) ;
  grid-auto-rows: minimax(50px, auto) ;
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.button {
  background-color: #F2F2F2;
  border: 1PX solid #999;
}
.operator {
  background-color: orange;
  color: white;
}

</style>
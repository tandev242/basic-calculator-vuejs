<template>
  <div class="p-3 wrapper">
    <div class="w-full rounded m-1 p-3 lead font-weight-bold result-board">
      {{ calculatorValue || 0}}
    </div>
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div class="bg-vue-dark text-center rounded hover-class text-white m-1 py-3"
          :class="{'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n)}"
          @click="action(n)"
        >
            {{n}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      calculatorValue: '',
      calculatorElements: ['C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.'],
      operator: null,
      previousCalculatorValue: ''
    }
  },
  methods: {
    action (n) {
      if(['/', '*', '-', '+'].includes(this.calculatorValue)){
        this.calculatorValue = ''
      }
      if (!isNaN(n) || n === '.') {
        this.calculatorValue += n + ''
      } else if (n === 'C') {
        this.calculatorValue = ''
      } else if (n === '%') {
        this.calculatorValue = this.calculatorValue / 100 + ''
      } else if (['/', '*', '-', '+'].includes(n)) {
        this.operator =n 
        this.previousCalculatorValue = this.calculatorValue
        this.calculatorValue = n
      } else {
        this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue)
        this.previousCalculatorValue = ''
        this.operator = null
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  max-width: 400px;
  background-color: aqua;
  border: 10px solid #ccc;
}
.result-board{
  background-color: rgb(235, 164, 223);
  text-align: right;
  font-weight: bold;
  font-size: 30px;
}
.bg-vue-dark {
  background-color: rgb(45, 16, 173);
}
.hover-class:hover{
  cursor: pointer;
  background-color: rgb(158, 206, 69);
}
.bg-vue-green {
  background-color: rgb(228, 128, 62);
}
</style>

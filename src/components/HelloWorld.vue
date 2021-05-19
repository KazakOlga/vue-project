<template>
  <div class="main">
    <input type="text" class="calculator_result" v-model.number="calculatorValue" value="0">
    <div class="checkbox">
      <input type="checkbox" class="check" id="checkbox" v-model="checked">
      <label for="checkbox">отобразить экранную клавиатуру</label>
    </div>
     <div class="container" v-show="checked">
       <div class="calculate_buttons" v-for="n in calculatorEls" :key="n" @click="input(n)">
       <div class="button" :class="{'operator' : ['C', '*', '/', '-', '+', 'parseInt', '=', 'pow'].includes(n)}" @click="calculate(n)">{{n}}</div>
     </div>
     </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      calculatorValue: '',
      calculatorEls: ['C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, 'parseInt', 1, 2, 3, '=', 0, 'pow'],
      operator: null,
      previousValue: '',
      checked: ''
    }
  },
  methods: {
    input (n) {
      if ([1, 2, 3, 4, 5, 6, 7, 8, 9, 0].includes(n)) {
        this.calculatorValue += n
      }
    },
    calculate (n) {
      if (n === 'C') {
        this.calculatorValue = ''
        this.operator = null
      }
      if (['parseInt', '*', '/', '-', '+', 'pow'].includes(n)) {
        this.operator = n
        this.previousValue = this.calculatorValue
        this.calculatorValue = ''
      }
      if (n === '=') {
        if (this.operator === '+') {
          this.calculatorValue = this.previousValue + this.calculatorValue
        }
        if (this.operator === '-') {
          this.calculatorValue = this.previousValue - this.calculatorValue
        }
        if (this.operator === '*') {
          this.calculatorValue = this.previousValue * this.calculatorValue
        }
        if (this.operator === '/') {
          this.calculatorValue = this.previousValue / this.calculatorValue
        }
        if (this.operator === 'parseInt') {
          this.calculatorValue = parseInt(this.previousValue / this.calculatorValue)
        }
        if (this.operator === 'pow') {
          this.calculatorValue = Math.pow(this.previousValue, this.calculatorValue)
        }
        this.previousValue = ''
        this.operator = null
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.main{
  width: 400px;
   margin: 50px auto;
  background: gray;
  padding: 5px;
  display: flex;
  flex-direction: column;
}
.calculator_result{
  text-align: right;
  padding: 5px;
  font-weight: bold;
  color: white;
  font-size: 25px;
  margin: 5px;
  background-color: yellowgreen;
}
.calculate_buttons{
  margin: 3px;
  padding: 3px;
}
.button{
width: 75px;
height:35px;
padding: 3px;
background-color: violet;
font-size: 18px;
color: white;
font-weight: bold;
}
.button:hover{
  cursor: pointer;
  background-color: aqua;
}
.container{
      display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
.operator{
  background-color: blue;
}
.checkbox{
  padding: 3px;
  background-color: yellowgreen;
  font-size: 20px;
  font-weight: bold;
  margin: 5px;
}
.check{
  display: none;
}
</style>

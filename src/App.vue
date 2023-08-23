<template>
  <div class="calculator">
    <div class="display ">
      <h1 v-text="calculatorDisplay" class="h-min text-7xl font-light overflow-x-auto rounded-md p-4"></h1>  
    </div>
    <div class="button-field">
      
        <button @click="reset" type="button" class="operator" value="">C</button>
        <button @click="percentage" type="button" class="operator" value="">%</button>
        <button @click="calculate('/')" type="button" class="operator" value="/">÷</button>
        <button @click="calculate('*')" type="button" class="operator" value="*">×</button>     
      
        <button @click="displayNumber('7')" type="button" value="7">7</button>
        <button @click="displayNumber('8')" type="button" value="">8</button>
        <button @click="displayNumber('9')" type="button" value="">9</button>
        <button @click="calculate('+')" type="button" class="operator" value="+">+</button>      
      
        <button @click="displayNumber('4')" type="button" value="">4</button>
        <button @click="displayNumber('5')" type="button" value="">5</button>
        <button @click="displayNumber('6')" type="button" value="">6</button>
        <button @click="calculate('-')" type="button" class="operator" value="-">-</button>      
      
        <button @click="displayNumber('1')" type="button" value="">1</button>
        <button @click="displayNumber('2')" type="button" value="">2</button>
        <button @click="displayNumber('3')" type="button" value="">3</button>
        <button @click="process" type="button" class="min-h-[50px] row-span-2 border-2 border-orange-600 rounded-md bg-red-600 text-white" value="">=</button>      
      
        <button @click="displayNumber('0')" type="button" value="">0</button>
        <button @click="toggleNegative" type="button" class="button" value="">+/-</button>
        <button @click="period" type="button" class="button" value="">.</button>
      
    </div>
  </div>
</template>

<script>
  export default {   
    // mounted(){
    //   const displayContent = this.$refs.display; 
    // },
      data() {
        return{
          previous: null,
          current: "",
          numberClicked: false,
          isNegative: false,
          hasBeenCalculated: false,
          result: null,
          // new try:
          calculatorDisplay: "0",
          displayValue: 0,
          isAwaitingInput: false,
          operate: {
            "+": (first, second) => first + second,
            "-": (first, second) => first - second,
            "/": (first, second) => first / second,
            "*": (first, second) => first * second,
            "=": (first, second) => first,
          },
          operatorValue: "",
        }
      },
      computed: {
        // const displayContent = this.$refs.display.textContent; 
      },  
      methods: {
        displayNumber(number){
          if(this.isAwaitingInput){
            this.calculatorDisplay = number;
            this.isAwaitingInput = false;
          } else {
            this.displayValue = this.calculatorDisplay;
            this.calculatorDisplay =
              this.displayValue === "0" ? number : this.displayValue + number;
          }
          this.displayValue = this.calculatorDisplay;
        },
        toggleNegative(){          
          this.displayValue = (parseFloat(this.displayValue) * -1).toString();
          this.calculatorDisplay = this.displayValue;
        },     
        period(){
          if (this.displayValue.includes(".")){
            return 
          } else {
            this.displayValue = `${this.displayValue}.`;
            this.calculatorDisplay = this.displayValue;
          }
        },
        calculate(operator){
          const followingValue = parseFloat(this.calculatorDisplay);
          // console.log("operator", operator);
          console.log("FirstfollowingValue", followingValue);
          // console.log("displayValue", this.displayValue);
          if(this.operatorValue && this.isAwaitingInput){
            this.operatorValue = operator;
            // console.log("operatorValue", this.operatorValue);            
            return;
          }
          
          if(!this.displayValue){
            this.displayValue = followingValue;
          } else {
            this.displayValue = parseFloat(this.displayValue);
            this.operatorValue = operator;
            const calculation = this.operate[ this.operatorValue](this.displayValue, followingValue);
            console.log("calculation", calculation);
            // console.log("operator", operator);
            // console.log("operatorValue", this.operatorValue);            
            console.log("displayValue", this.displayValue);
            console.log("followingValue", followingValue);
            this.calculatorDisplay = calculation;
            this.displayValue = calculation;
          }
          this.isAwaitingInput = true;
          this.operatorValue = operator;
          console.log("operatorValue", this.operatorValue);            
          console.log("type of operatorValue", typeof(this.operatorValue));            
        },   
      }    
  }
</script>

<style></style>

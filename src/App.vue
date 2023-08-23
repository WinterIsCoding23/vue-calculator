<template>
  <div class="calculator">
    <div class="display ">
      <h1 v-text="calculatorDisplay || 0" class="h-min text-7xl font-light overflow-x-auto rounded-md p-4"></h1>  
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
      data() {
        return{
          previous: null,
          calculatorDisplay: "",
          displayValue: 0,
          isAwaitingInput: false,
          operatorValue: "",
        }
      },
      methods: {
        displayNumber(number) {
          if(this.isAwaitingInput){
            this.calculatorDisplay = "";
            this.isAwaitingInput = false;
          }
          // if (this.isAwaitingInput) {
          //   this.calculatorDisplay = number;
          //   this.isAwaitingInput = false;
          // } else {
          //   if (this.operatorValue) {
          //     this.calculatorDisplay += number; 
          //   } else {
          //     this.displayValue = this.calculatorDisplay;
          //     this.calculatorDisplay = this.displayValue === "0" ? number : this.displayValue + number;
          //   }
          // }
          this.calculatorDisplay = `${this.calculatorDisplay}${number}`;
        },

        toggleNegative(){  
          this.calculatorDisplay = (parseFloat(this.calculatorDisplay) * -1).toString();       
          // this.displayValue = (parseFloat(this.displayValue) * -1).toString();
          // this.calculatorDisplay = this.displayValue;
        },     
        period(){
          if(this.calculatorDisplay.includes(".")){
            return;
          } else {
            this.calculatorDisplay = `${this.displayValue}.`;
          }
          // if (this.displayValue.includes(".")){
          //   return; 
          // } else {
          //   this.displayValue = `${this.displayValue}.`;
          //   this.calculatorDisplay = this.displayValue;
          // }
        },
        setPrevious(){
          this.previous = this.calculatorDisplay;
          this.isAwaitingInput = true;
          // this.previous = this.displayValue;
          // console.log("previous", this.previous);
          // console.log("previous-displayValue", this.displayValue);
          // this.isAwaitingInput = true;
          // return this.previous;
        },
        calculate(operator) {

          // if (this.operatorValue && this.isAwaitingInput) {
          //   this.operatorValue = operator;
          //   return;
          // }

          // if (!this.operatorValue) {
          //   this.setPrevious(); 
          // } else {
          //   const followingValue = parseFloat(this.calculatorDisplay);
            
          //   switch (this.operatorValue) {
          //     case "+":
          //       this.displayValue = this.previous + followingValue;
          //       console.log("displayValue in switch", this.displayValue);
          //       this.setPrevious(); 
          //       break;
          //     case "-":
          //       this.displayValue = this.previous - followingValue;
          //       break;
          //     case "*":
          //       this.displayValue = this.previous * followingValue;
          //       break;
          //     case "/":
          //       this.displayValue = this.previous / followingValue;
          //       break;             
          //   }
          // }
          // this.operatorValue = operator;
          // this.calculatorDisplay += operator;
          // this.isAwaitingInput = true;
        }
      }
  }    
</script>

<style></style>

<template>
  <div class="calculator">
    <div class="display ">
      <h1 v-text="calculatorDisplay" class="h-min text-7xl font-light overflow-x-auto rounded-md p-4"></h1>  
    </div>
    <div class="button-field">
      
        <button @click="reset" type="button" class="operator" value="">C</button>
        <button @click="percentage" type="button" class="operator" value="">%</button>
        <button @click="operate('/')" type="button" class="operator" value="/">÷</button>
        <button @click="operate('*')" type="button" class="operator" value="*">×</button>     
      
        <button @click="displayNumber('7')" type="button" value="7">7</button>
        <button @click="displayNumber('8')" type="button" value="">8</button>
        <button @click="displayNumber('9')" type="button" value="">9</button>
        <button @click="operate('+')" type="button" class="operator" value="+">+</button>      
      
        <button @click="displayNumber('4')" type="button" value="">4</button>
        <button @click="displayNumber('5')" type="button" value="">5</button>
        <button @click="displayNumber('6')" type="button" value="">6</button>
        <button @click="operate('-')" type="button" class="operator" value="">-</button>      
      
        <button @click="displayNumber('1')" type="button" value="">1</button>
        <button @click="displayNumber('2')" type="button" value="">2</button>
        <button @click="displayNumber('3')" type="button" value="">3</button>
        <button @click="calculate" type="button" class="min-h-[50px] row-span-2 border-2 border-orange-600 rounded-md bg-red-600 text-white" value="">=</button>      
      
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
          displayValue: "0",
          isAwaitingInput: false,
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
            this.displayValue = this.calculatorDisplay;
            console.log("calculatorDisplay", this.calculatorDisplay);
            console.log("number", number);
          } else {
            this.displayValue = this.calculatorDisplay;
            this.calculatorDisplay =
              this.displayValue === "0" ? number : this.displayValue + number;
            this.displayValue = this.calculatorDisplay;
            console.log("displayValue", this.displayValue);
            console.log("number", number);
          }
        },
        toggleNegative(){          
          this.displayValue = (parseInt(this.displayValue) * -1).toString();
          this.calculatorDisplay = this.displayValue;
        },        
      }    
  }
</script>

<style></style>

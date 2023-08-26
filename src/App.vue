<template>
  <div class="calculator">
    <div class="display ">
      <h1 v-text="current || 0" class="h-min text-7xl font-light overflow-x-auto rounded-md p-4"></h1>  
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
        <button @click="operate('-')" type="button" class="operator" value="-">-</button>      
      
        <button @click="displayNumber('1')" type="button" value="">1</button>
        <button @click="displayNumber('2')" type="button" value="">2</button>
        <button @click="displayNumber('3')" type="button" value="">3</button>
        <button @click="displayResult" type="button" class="min-h-[50px] row-span-2 border-2 border-orange-600 rounded-md bg-red-600 text-white" value="">=</button>      
      
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
          current: "",
          calculatorDisplay: "",
          interimResult: 0,
          operatorWasClicked: false,
          operatorValue: null,
          operatorClicked: null,
          isAwaitingNumber: false,
        }
      },
      methods: {
        setPrevious(){
          this.previous = this.current;
          this.operatorWasClicked = true;  
        },

        displayNumber(number) {
          if(this.operatorWasClicked){
            this.current = "";
            this.operatorWasClicked = false;
          }
          this.current = `${this.current}${number}`;
        },
 
        toggleNegative(){  
          this.current = (parseFloat(this.current) * -1).toString();       
        },     
        period(){
          if(this.current.includes(".")){
            return;
          } else {
            this.current = `${this.current}.`;
          }
        },  
        
        add(){
          
        },
        subtract(){
          
        },
        multiply(){
          
        },
        divide(){
          
        },

        operate(operator){  
             
        },

        reset(){
          this.calculatorDisplay = "";
          this.interimResult = 0;
          this.current = "";
          this.previous = "";
          this.operatorWasClicked = false;
          console.log("calculatorDisplay", this.calculatorDisplay);
          console.log("interimResult", this.interimResult);
        },
        
        displayResult(){
          this.calculatorDisplay = this.interimResult;
          this.operatorWasClicked = false;
        },
    }
  }    
</script>

<style></style>

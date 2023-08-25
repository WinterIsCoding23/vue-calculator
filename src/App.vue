<template>
  <div class="calculator">
    <div class="display ">
      <h1 v-text="calculatorDisplay || 0" class="h-min text-7xl font-light overflow-x-auto rounded-md p-4"></h1>  
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
          this.previous = this.calculatorDisplay;
        },

        displayNumber(number) {
          const operators = ["+", "-", "*", "/"];
          if(this.previous){
            if(operators.includes(this.previous[this.previous.length - 1])){            
              for (const operator of operators) {
                if (this.calculatorDisplay.includes(operator)) {
                  this.operatorClicked = operator;
                  console.log("operatorClicked", this.operatorClicked);
                  break;
                }
              }
  
              if (this.operatorClicked === "+") {
                this.add(number);
              } else if (this.operatorClicked === "-") {
                this.subtract(number);  
              } else if (this.operatorClicked === "*") {
                this.multiply(number);
              } else if (this.operatorClicked === "/") {
                this.divide(number);
              }
                this.operatorWasClicked = false;
                this.setPrevious();
              } else {
                this.calculatorDisplay = this.previous ? `${this.previous}${number}` : number;
                this.interimResult = Number(this.calculatorDisplay);
                this.setPrevious();
              }
          } else {
            this.calculatorDisplay = number;
            this.interimResult = number;
            this.setPrevious();
          }      
          console.log("this.previous after", this.previous);
          console.log("this.interimResult", this.interimResult);
        },
 
        toggleNegative(){  
          this.calculatorDisplay = (parseFloat(this.calculatorDisplay) * -1).toString();       
        },     
        period(){
          if(this.calculatorDisplay.includes(".")){
            return;
          } else {
            this.calculatorDisplay = `${this.calculatorDisplay}.`;
          }
          this.setPrevious();
        },  
        
        add(number){
          this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = Number(this.interimResult) + Number(number);
        },
        subtract(number){
          this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = Number(this.interimResult) - Number(number);   
        },
        multiply(number){
          this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = Number(this.interimResult) * Number(number);
        },
        divide(number){
          this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = number !== 0 ? Number(this.interimResult) / Number(number) : alert("Pendejo!");
        },

        operate(operator){     
          if (!this.operatorWasClicked && this.calculatorDisplay === ""){
            console.log("first case");
            this.interimResult = 0;
            this.calculatorDisplay = `0${operator}`;
            this.operatorClicked = operator;
            this.setPrevious();
            this.operatorWasClicked = true;
            this.isAwaitingNumber = true;
          } else if(!this.operatorWasClicked){
            console.log("second case");
            this.interimResult = this.calculatorDisplay;
            this.calculatorDisplay = `${this.calculatorDisplay}${operator}`;
            this.operatorClicked = operator;
            this.setPrevious();
            this.operatorWasClicked = true;
            this.isAwaitingNumber = true;
          } else {
            console.log("third case");
            return;
          }  
          console.log("interimResult", this.interimResult);
          console.log("calculatorDisplay", this.calculatorDisplay);        
        },

        reset(){
          this.calculatorDisplay = "";
          this.interimResult = 0;
          console.log("calculatorDisplay", this.calculatorDisplay);
          console.log("interimResult", this.interimResult);
        },
        
        displayResult(){
          this.calculatorDisplay = this.interimResult;
        },
    }
  }    
</script>

<style></style>

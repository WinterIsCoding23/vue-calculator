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
          // this.previous = this.calculatorDisplay;
          this.previous = this.current;
          this.current = "";
        },

        displayNumber(number) {
          const operators = ["+", "-", "*", "/"];
          console.log("current in displayNumber", this.current);
          console.log("operatorWasClicked", this.operatorWasClicked);
          if(this.previous){
            if(this.operatorWasClicked){            
              for (const operator of operators) {
                if (this.calculatorDisplay.includes(operator)) {
                  this.operatorClicked = operator;
                  console.log("operatorClicked", this.operatorClicked);
                  break;
                }
              }
              if (this.operatorClicked === "+") {
                this.current = number;
                this.interimResult = Number(this.previous)+Number(this.current);
                console.log("interimResult in displayNumber", this.interimResult);
              } else if (this.operatorClicked === "-") {
                this.subtract(number);  
              } else if (this.operatorClicked === "*") {
                this.multiply(number);
              } else if (this.operatorClicked === "/") {
                this.divide(number);
              }
            }

            // this.current = `${this.previous}${number}`;
            // this.calculatorDisplay = `${this.previous}${number}`;
            // // this.interimResult = Number(this.calculatorDisplay);
            // this.setPrevious();
            // if(operators.includes(this.previous[this.previous.length - 1])){            
            //   for (const operator of operators) {
            //     if (this.calculatorDisplay.includes(operator)) {
            //       this.operatorClicked = operator;
            //       console.log("operatorClicked", this.operatorClicked);
            //       break;
            //     }
            //   }
  
            //   if (this.operatorClicked === "+") {
            //     this.add(number);
            //   } else if (this.operatorClicked === "-") {
            //     this.subtract(number);  
            //   } else if (this.operatorClicked === "*") {
            //     this.multiply(number);
            //   } else if (this.operatorClicked === "/") {
            //     this.divide(number);
            //   }
            //     this.operatorWasClicked = false;
            //     this.setPrevious();
            //   } else {
            //     this.calculatorDisplay = this.previous ? `${this.previous}${number}` : number;
            //     this.interimResult = Number(this.calculatorDisplay);
            //     this.setPrevious();
            //   }
          } else {
            this.current = number;
            this.calculatorDisplay = number;
            this.interimResult = Number(number);
            // this.setPrevious();
          }      
          console.log("previous displayNumber end", this.previous);
          console.log("current displayNumber end", this.current);
          console.log("this.interimResult", this.interimResult);
        },
 
        toggleNegative(){  
          this.calculatorDisplay = (parseFloat(this.calculatorDisplay) * -1).toString();       
        },     
        period(){
          if(this.calculatorDisplay.includes(".")){
            return;
          } else {
            this.calculatorDisplay = `${this.previous}.`;
            this.current = `${this.previous}.`;
          }
          this.setPrevious();
        },  
        
        add(){
          this.calculatorDisplay = `${this.previous}+`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          // this.current = `${this.previous}+`;
          this.operatorWasClicked = true;
          this.previous = this.current;
          this.current = "";
          console.log("current in add", this.current);
          console.log("previous in add", this.previous);
          // this.interimResult = Number(this.previous) + Number(this.current);
        },
        subtract(){
          // this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = Number(this.interimResult) - Number(this.current);   
        },
        multiply(){
          // this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = Number(this.interimResult) * Number(this.current);
        },
        divide(){
          // this.calculatorDisplay = `${this.previous}${number}`;
          console.log("this.calculatorDisplay", this.calculatorDisplay);
          this.interimResult = this.current !== 0 ? Number(this.interimResult) / Number(this.current) : alert("Pendejo!");
        },

        operate(operator){  
          console.log("current", this.current); 
          const operators = ["+", "-", "*", "/"];
          if(!operators.includes(this.calculatorDisplay[this.calculatorDisplay.length - 1])){            
              // for (const operator of operators) {
              //   if (this.calculatorDisplay.includes(operator)) {
              //     this.operatorClicked = operator;
              //     console.log("operatorClicked", this.operatorClicked);
              //     break;
              //   }
              // }

              if (operator === "+") {
                this.previous = this.current;
                this.calculatorDisplay = `${this.current}${operator}`;  
                this.operatorWasClicked = true;
                console.log("previous in operate", this.previous);
                console.log("current in operate", this.current);
              } else if (this.operatorClicked === "-") {
                this.subtract();  
              } else if (this.operatorClicked === "*") {
                this.multiply();
              } else if (this.operatorClicked === "/") {
                this.divide();
              }

                // this.calculatorDisplay = `${this.previous}${operator}${this.current}`
                this.operatorWasClicked = false;
                // this.setPrevious();
                // console.log("previous in operate", this.previous);
                // console.log("current in operate", this.current);

          } else {
              return;
          }

          // if (!this.operatorWasClicked && this.calculatorDisplay === ""){
          //   console.log("first case");
          //   this.interimResult = 0;
          //   this.calculatorDisplay = `0${operator}`;
          //   this.operatorClicked = operator;
          //   this.setPrevious();
          //   this.operatorWasClicked = true;
          //   this.isAwaitingNumber = true;
          // } else if(!this.operatorWasClicked){
          //   console.log("second case");
          //   this.interimResult = this.calculatorDisplay;
          //   this.calculatorDisplay = `${this.calculatorDisplay}${operator}`;
          //   this.operatorClicked = operator;
          //   this.setPrevious();
          //   this.operatorWasClicked = true;
          //   this.isAwaitingNumber = true;
          // } else {
          //   console.log("third case");
          //   return;
          // }  
          // console.log("interimResult", this.interimResult);
          // console.log("calculatorDisplay", this.calculatorDisplay);        
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

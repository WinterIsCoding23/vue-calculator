<template>
  <div class="calculator">
    <div class="display ">
      <h1 v-text="current || 0" class="h-min text-3xl tiny:text-4xl sm:text-7xl font-light overflow-x-auto rounded-md p-4"></h1>  
    </div>
    <div class="button-field">
      
        <button @click="reset" type="button" class="operator" value="">C</button>
        <button @click="percentage" type="button" class="operator" value="">%</button>
        <button @click="divide" type="button" class="operator" value="/">÷</button>
        <button @click="multiply" type="button" class="operator" value="*">×</button>     
      
        <button @click="displayNumber('7')" type="button" value="7">7</button>
        <button @click="displayNumber('8')" type="button" value="">8</button>
        <button @click="displayNumber('9')" type="button" value="">9</button>
        <button @click="add" type="button" class="operator" value="+">+</button>      
      
        <button @click="displayNumber('4')" type="button" value="">4</button>
        <button @click="displayNumber('5')" type="button" value="">5</button>
        <button @click="displayNumber('6')" type="button" value="">6</button>
        <button @click="subtract" type="button" class="operator" value="-">-</button>      
      
        <button @click="displayNumber('1')" type="button" value="">1</button>
        <button @click="displayNumber('2')" type="button" value="">2</button>
        <button @click="displayNumber('3')" type="button" value="">3</button>
        <button @click="displayResult" type="button" class="min-h-[50px] row-span-2 border-2 border-orange-600 rounded-md bg-[#C51605] dark:bg-red-600 text-white" value="">=</button>      
      
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
          operatorWasClicked: false,
          operator: null,
        }
      },
      methods: {
        formatWithCommas(numberString) {
          const parts = numberString.split(".");
          let integerPart = parts[0] || "";
          const decimalPart = parts[1] || "";

          if (integerPart.charAt(0) === "-") {
            integerPart = "-" + integerPart.slice(1).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
          } else {
            integerPart = integerPart.replace(/\B(?=(\d{3})+(?!\d))/g, ",");
          }

          return integerPart + (decimalPart ? "." + decimalPart : "");
        },

        setPrevious(){
          this.current = this.current.replace(/,/g, '');
          this.previous = this.current;
          this.operatorWasClicked = true;  
        },
        displayNumber(number) {
          if(this.operatorWasClicked){
            this.current = "";
            this.operatorWasClicked = false;
          }
          this.current = this.current.replace(/,/g, '');
          this.current = `${this.current}${number}`;
          this.current = this.formatWithCommas(this.current);
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
          this.operator = (previous, current) => previous + current; 
          this.setPrevious();
        },
        subtract(){
          this.operator = (previous, current) => previous - current; 
          this.setPrevious();
        },
        multiply(){
          this.operator = (previous, current) => previous * current; 
          this.setPrevious();
        },
        divide(){
          this.operator = (previous, current) => previous / current; 
          this.setPrevious();
        },
        reset(){
          this.current = "";
        },        
        displayResult(){
          this.current = this.previous ? `${this.operator(parseFloat(this.previous), parseFloat(this.current))}` : this.current;
          this.current = this.formatWithCommas(this.current);
          this.previous = null;
        },
    }
  }    
</script>

<style></style>

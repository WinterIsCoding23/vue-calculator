<template>
  <div class="calculator">
    <div class="display ">
      <h1 class="h-min text-7xl font-light overflow-x-auto rounded-md p-4">{{ current || 0 }}</h1>  
    </div>
    <div class="button-field">
      
        <button @click="reset" type="button" class="operator" value="">C</button>
        <button @click="percentage" type="button" class="operator" value="">%</button>
        <button @click="operate('/')" type="button" class="operator" value="/">÷</button>
        <button @click="operate('*')" type="button" class="operator" value="*">×</button>     
      
        <button @click="display(7)" type="button" value="7">7</button>
        <button @click="display(8)" type="button" value="">8</button>
        <button @click="display(9)" type="button" value="">9</button>
        <button @click="operate('+')" type="button" class="operator" value="+">+</button>      
      
        <button @click="display(4)" type="button" value="">4</button>
        <button @click="display(5)" type="button" value="">5</button>
        <button @click="display(6)" type="button" value="">6</button>
        <button @click="operate('-')" type="button" class="operator" value="">-</button>      
      
        <button @click="display(1)" type="button" value="">1</button>
        <button @click="display(2)" type="button" value="">2</button>
        <button @click="display(3)" type="button" value="">3</button>
        <button @click="calculate" type="button" class="min-h-[50px] row-span-2 border-2 border-orange-600 rounded-md bg-red-600 text-white" value="">=</button>      
      
        <button @click="display(0)" type="button" value="">0</button>
        <button @click="negative" type="button" class="button" value="">+/-</button>
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
          numberClicked: false,
          isNegative: false,
          hasBeenCalculated: false,
          result: null,
        }
      },
      methods: {
        display(number){
          if(this.hasBeenCalculated){
            this.reset();
            this.current = number;
            this.hasBeenCalculated = false;
            console.log("hasBeenCalculated", this.hasBeenCalculated);
          } else{
            if(this.previous){
              this.current = this.previous.toString().concat("", number);
            } else {
              this.current = number;
            }
          }
          this.numberClicked = true;  
          this.previous = this.current;
          console.log("this.current", this.current);
          console.log("this.previous", this.previous);
        },
        negative(){
          if(this.isNegative){
            this.current = this.current.split("-")[1];
            this.isNegative = false;
            this.previous = this.current;
          } else {
            this.current = `-${this.current}`;
            this.isNegative = true;
            this.previous = this.current;
          }
        },
        period(){
          this.current.toString().split("").includes(".") ? this.current : this.current = `${this.current}.`;  
          this.previous = this.current;
        },
        percentage(){
          // to be fixed: adding % after a calculation
          this.current = parseFloat(this.current)/100;
        },
        operate(operator){
        if(this.numberClicked){
          this.current += operator;
          this.previous = this.current;
          this.numberClicked = false;
          this.hasBeenCalculated = false;
          console.log("this.current operate", this.current);
          console.log("hasBeenCalculated operate", this.hasBeenCalculated)
        } return;
        },
        deleteFunction(){
          this.current = this.current.toString();
          this.current = this.current.slice(0, -1); 
          return this.current;
        },
        reset(){
          this.current = "";
          this.previous = null;
        },
        calculate(){
          // to be fixed: replace eval
          this.current = eval(this.current);
          this.previous = this.current;
          this.hasBeenCalculated = true;
        },
      }    
  }
</script>

<style></style>

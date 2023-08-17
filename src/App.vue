<template>
  <div class="calculator">
    <div class="display ">
      <h1 class="h-min text-7xl font-light overflow-x-auto rounded-md p-4">{{ current || 0 }}</h1>  
    </div>
    <div class="button-field">
      
        <button type="button" class="operator" value="">C</button>
        <button type="button" class="operator" value="">%</button>
        <button type="button" class="operator" value="/">÷</button>
        <button type="button" class="operator" value="*">×</button>     
      
        <button @click="display(7)" type="button" value="7">7</button>
        <button @click="display(8)" type="button" value="">8</button>
        <button @click="display(9)" type="button" value="">9</button>
        <button type="button" class="operator" value="">+</button>      
      
        <button @click="display(4)" type="button" value="">4</button>
        <button @click="display(5)" type="button" value="">5</button>
        <button @click="display(6)" type="button" value="">6</button>
        <button type="button" class="operator" value="">-</button>      
      
        <button @click="display(1)" type="button" value="">1</button>
        <button @click="display(2)" type="button" value="">2</button>
        <button @click="display(3)" type="button" value="">3</button>
        <button type="button" class="min-h-[50px] row-span-2 border-2 border-orange-600 rounded-md bg-red-600 text-white" value="">=</button>      
      
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
        }
      },
      methods: {
        display(number){
          if(this.isNegative && this.previous !== null){
            this.current = `${this.previous}${number}`;
          } else if(this.isNegative && this.previous === null){
            this.current = -number;
          } else if(!this.isNegative && this.previous !== null){
            this.current = `${this.previous}${number}`;
          } else {
            this.current = number;
          }
          this.numberClicked = true;  
          this.previous = this.current;

          console.log("this.current", this.current);
        },
        negative(){
          // if already number clicked, then make it negative
          // ...if this number is negative, then make it positive
          // if (this.numberClicked){
          //   this.current = -this.current;
          //   this.isNegative = true;
          // } else {
          // this.isNegative = true;
          // }
          console.log("previous before", this.previous);
          console.log("isNegative before", this.isNegative);
          console.log("current before", this.current);
          this.previous ? this.current = -1*this.previous : this.isNegative === true;
          console.log("previous after", this.previous);
          console.log("isNegative after", this.isNegative);
          console.log("current after", this.current);
        },
        period(){
          if(this.numberClicked){
            this.previous = `${this.current}.`;
          } else {
            this.previous = 0+".";
            // this.current = 0+".";
          }
          console.log("this.current period", this.current);
          console.log("this.previous period", this.previous);
        }
      }    
  }
</script>

<style></style>

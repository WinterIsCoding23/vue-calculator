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
        <button type="button" class="button" value="">+/-</button>
        <button type="button" class="button" value="">.</button>
      
    </div>
  </div>
</template>

<script>
  export default {   
      data() {
        return{
          previous: null,
          current: "",
        }
      },
      methods: {
        display(number){
          this.current = number;
          console.log("this.current", this.current);
          console.log("number", number);
        }
      }    
  }
</script>

<style></style>

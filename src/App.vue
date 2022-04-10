<template>
  <div class="calculator">
    <div class="screen">
      {{calcValue}}
    </div>
    <div  class="buttons">
      <div 
        v-for="value in buttons" 
        :key="value" 
        class="button"
        @click="action(value)"
      >
        {{value}}
      </div> 
    </div>
  </div>
</template>

<script>
export default {
data() {
  return {
    buttons: ["C", "%", "/", "*", 1, 2, 3,"-", 4, 5, 6, "+", 7, 8, 9, "=", 0, "."],
    calcValue: "",
    operator: "",
    prevValue: ""
  }
},

methods: {
  action(value) {

    if (!isNaN(value) || value === ".") {
      this.calcValue += value + ""
    }

    if (value === "C") {
      this.calcValue = ""
    } 

    if (value === "%") {
      this.calcValue = this.calcValue / 100 + ""
    } 

    if (["/", "*", "-", "+",].includes(value)) {
      this.operator = value
      this.prevValue = this.calcValue
      this.calcValue = ""
    }

    if (value === "=") {
      this.calcValue = eval(
        this.prevValue + this.operator + this.calcValue
      )

      this.prevValue = ""
      this.operator = null
    }
  }
}
}
</script>

<style>
body {
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Inter', sans-serif;
  font-weight: 200;
  box-sizing: border-box;
}
.calculator {
  
  width: 320px;
  min-height: 600px;
  padding: 10px;
  background: #000;
  color: white;
}

.screen {
  
  height: 150px;
  font-size: 35px;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  padding: 15px;
  box-sizing: border-box;
}

.buttons {
  display: flex;
  flex-wrap: wrap;
  margin-top: 10px;
  
}

.button {
  font-size: 60px;
  width: 80px;
  height: 80px;  
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
}

.button:hover {
   background-color: #333333;
}
</style>
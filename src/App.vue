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
    buttons: ["C", "*", "/", "-", 1, 2, 3, "+", 4, 5, 6, "%", 7, 8, 9, "=", 0, "."],
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

    if (["/", "*", "-", "+"].includes(value)) {
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
  background: rgba(0, 0, 0, 0.893);
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}
.calculator {
  border: 2px solid white;
  width: 400px;
  height: 600px;
  padding: 10px;
}

.screen {
  border: 2px solid white;
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
  color: white;
  border: 2px solid white;
  font-size: 60px;
  width: 80px;
  height: 80px;  
  margin: 0 10px 10px 0;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  background: transparent;
}
</style>
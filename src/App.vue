<template>
 <div class="container">
  <div class="calculator">
      <div class="display">{{current || 0}}</div>
      <div @click="clear" class="btn">AC</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="percent" class="btn">%</div>
      <div @click="divide" class="btn operator">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="multiply" class="btn operator">*</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="plus" class="btn operator">+</div>
      <div @click="append('0')" class="btn zero">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator"> =</div>
  </div>
 </div>
</template>

<script>

export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods:{
    clear(){
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? 
      this.current.slice(1): `-${this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(num){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    dot(){
      if(this.current.indexOf('.') === -1){
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a, b) => a - b < 0 ? -(a-b) : (a-b);
      this.setPrevious();
    },
    plus(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`;
      this.previous = null;
    }
  }
}
</script>

<style>
body{
  background-image: linear-gradient(to right ,#D1913C, #FFD194);
  color: white;
}

.calculator{
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  margin: 100px auto;
  width: 400px;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  text-align: center;
}

.display{
  grid-column: 1/5;
  background-color: teal;
  border-radius: 6px;
  border:  2px inset coral ;
  text-shadow: 2px 2px orange;
}

.zero{
  grid-column: 1/3;
}

.btn{
  background-color: #f2f2f2;
  border: 1px outset coral;
  cursor: pointer;
  font-size: 18px;
}

.btn:hover{
  background-color: orange;
  color: white;
}

.operator{
  background-color: orange;
  color: white;
  border: 1px outset coral;
}

.operator:hover{
  background-color: white;
  color: black;
}

</style>

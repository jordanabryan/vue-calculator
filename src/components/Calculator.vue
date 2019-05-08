<template>
  <div class="calculator">
    <div class='display'>{{ current || 0 }}</div>
    <div class='button' @click="clear">AC</div>
    <div class='button' @click="sign">+/-</div>
    <div class='button' @click="percent">%</div>
    <div class='button operator' @click="divide">&divide;</div>
    <div class='button' @click="append('7')">7</div>
    <div class='button' @click="append('8')">8</div>
    <div class='button' @click="append('9')">9</div>
    <div class='button operator' @click="times">&times;</div>
    <div class='button' @click="append('4')">4</div>
    <div class='button' @click="append('5')">5</div>
    <div class='button' @click="append('6')">6</div>
    <div class='button operator' @click="divide">&minus;</div>
    <div class='button' @click="append('3')">3</div>
    <div class='button' @click="append('2')">2</div>
    <div class='button' @click="append('1')">1</div>
    <div class='button operator' @click="add">&plus;</div>
    <div class='button zero' @click="append('0')">0</div>
    <div class='button' @click="dot">.</div>
    <div class='button operator' @click="equal ">&equals;</div>
  </div>
</template>

<script>

export default {
  name: 'Calculator',
  data(){
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
      clear(){
        this.current = ''
      },
      sign(){
        this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
      },
      percent(){
        this.current = `${parseFloat(this.current) / 100}`;
      },
      append(number){
        if(this.operatorClicked){
          this.current = '';
          this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`
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
      times(){
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },
      minus(){
        this.operator = (a, b) => a - b;
        this.setPrevious();
      },
      add(){
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

<style scoped lang='scss'>

.calculator{
  width: 300px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 30px;
  border: 1px solid #8f8f8f;

  .display{
    grid-column: 1 / 5;
    text-align: right;
    padding: 5px 10px;
    background-color: #4c4c4c;
    color: #fff;
    height: 100;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    font-size: 50px;
  }

  .button{
    background-color: #e0e0e0;
    border: 0.5px solid #8f8f8f;
    cursor: pointer;
    height: 75px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .operator{
    background-color: #f79232;
    color: #fff;
  }

  .zero{
    grid-column: 1 / 3;
  }

}

</style>

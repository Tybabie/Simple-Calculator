<template>
    <div id="calculator">
        <div  id='display'>{{current || 0}}</div>
        <div @click="clear" class="black">MC</div>
        <div @click="sign" class="black">M+</div>
        <div @click="divide" class="black">÷</div>
        <div @click="times" class="black">×</div>
        <div @click="append(7)" class="grey">7</div>
        <div @click="append(8)" class="grey">8</div>
        <div @click="append(9)" class="grey">9</div>
        <div @click="minus" class="grey">-</div>
        <div @click="append(4)" class="grey">4</div>
        <div @click="append(5)" class="grey">5</div>
        <div @click="append(6)" class="grey">6</div>
        <div @click="plus" class="grey">+</div>
        <div @click="append(1)" class="grey">1</div>
        <div @click="append(2)"  class="grey">2</div>
        <div @click="append(3)" class="grey">3</div>
        <div @click="equal" id="equal">=</div>
        <div @click="leadingZero"  id='zero'>0</div>
        <div @click ='dot' class="grey">.</div>
        
       
    </div>
</template>
<script>
export default {
  name: 'Calculator',
  data () {
    return {
      previous: null,
      operator: null,
      current: '',
      operatorClicked: false
    }
  },
  methods: {
    clear(){
      this.current = ''
    },
    sign(){
      if(this.current.charAt(0) === '-'){
        this.current = this.current.slice(1)
      }
      else{
        this.current = `-${this.current}`
      }
    },
    leadingZero(){
      this.append('0')
    },
    append(fig){

     if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      if (this.current.length < 20) {
        this.current = `${this.current}${fig}`;
      }
      
    },
    dot(){
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    plus(){
      this.operator = (a,b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus(){
    this.operator = (a,b) => a - b;
    this.previous = this.current;
      this.operatorClicked = true;
    },
    times(){
      this.operator = (a,b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a,b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal(){
    this.current = this.operator(parseFloat(this.previous), parseFloat(this.current))
    
    },
  
  }
}
</script>

<style scoped>
#calculator{
  margin: 50px auto;
    width: 300px;
    display: grid;
    grid-template-columns: auto auto auto auto;
    grid-template-areas: '. . . . ' '. . . .' '. . . .''. . . .' '. . . myArea ' '. . . myArea ';
    background-color: rgb(57, 57, 59);
    border-radius: 20px;
    color: white;
    padding: 20px;
    grid-gap: 10px;
  text-align: center;
  font-size: 25px;
}
.grey{
  background-color: rgb(88, 89, 91);
  padding: 10px 0px;
  cursor: pointer;
  outline: none;
}
.grey:hover{
  background-color: rgb(241, 90, 43);
}
#display{
  grid-column: 1/5;
  margin: 10px 0px;
 padding: 20px;
 background-color: rgb(88, 89, 91);
 border-radius: 10px;
 text-align: right;
 cursor: text;
}
#zero{
  grid-column: 1/3;
  background-color: rgb(88, 89, 91);
  padding: 10px 0px;
  cursor: pointer;
}
#zero:hover{
  background-color: rgb(241, 90, 43);
}
#equal{
 grid-area: myArea;
 padding: 50px 0px;
background-color: rgb(241, 90, 43);
cursor: pointer;
}
#equal:hover{
 background-color: rgb(211, 62, 17);
}
.black{
  background-color: black;
  margin: 10px 0px;
    padding: 10px 0px;
    cursor: pointer;
}
.black:hover{
  background-color: rgb(241, 90, 43) ;
}
</style>
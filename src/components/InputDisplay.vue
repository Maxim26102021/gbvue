<template>
  <div class='inputs'>
    <label for='operand1' class='box'>
      <p>first operand</p>
      <input type='text' id='operand1' v-model.number='operand1'>
    </label>
    <label for='operand2' class='box'>
      <p>second operand</p>
      <input type='text' id='operand2' v-model.number='operand2'>
    </label>
    <div class='btns'>
      <Buttons @custom-event='start'
               v-for='(operation, indx) in operations'
               :operation='operation'
               :show='operationDisabled'
               :key='indx' />
    </div>
    <div class='result'>{{ result }}</div>
    <Numbers @press-num='inpNum'/>
    <div class='radio'>
      <p>first input<input v-on:change='changeInput($event.target.value)' type='radio' name='choose' value='operand1'></p>
      <p>second input<input v-on:change='changeInput($event.target.value)' type='radio' name='choose' value='operand2'></p>
    </div>
  </div>
</template>

<script>
import Buttons from '@/components/Buttons';
import Numbers from '@/components/Numbers';

export default {
  data() {
    return {
      operand1: '',
      operand2: '',
      result: '',
      currentOperand: 'operand1',
      operations: ['+', '-', '*', '/', '%', '**']
    };
  },
  components: {
    Buttons,
    Numbers
  },
  methods: {
    start(event) {
      this.operand1 = +this.operand1;
      this.operand2 = +this.operand2;
      if (typeof (this.operand1) == 'string' || typeof (this.operand2) == 'string') {
        this.result = 'Not a Number';
        return;
      } else {
        switch (event) {
          case '+':
            this.result = this.operand1 + this.operand2;
            break;
          case '-':
            this.result = this.operand1 - this.operand2;
            break;
          case '*':
            this.result = this.operand1 * this.operand2;
            break;
          case '/':
            this.result = this.operand1 / this.operand2;
            break;
          case '%':
            this.result = this.operand1 % this.operand2;
            break;
          case  '**':
            this.result = Math.pow(this.operand1, this.operand2)
        }
      }
    },
    changeInput(val) {
      this.currentOperand = val
    },
    inpNum(num) {
      console.log(num)
     this[this.currentOperand] += num
    }
  },
  computed: {
    operationDisabled: function() {
      if (this.operand1 && this.operand2) return false;
      else return true;
    }
  }
};

</script>

<style>
.inputs {
  margin: 0 auto;
  width: 400px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.box {
  width: 300px;
  display: flex;
  height: 30px;
  align-items: center;
  justify-content: space-between;
}

.btns {
  margin-top: 5px;
  display: flex;
  justify-content: space-between;
}
.result {
  border: 1px solid grey;
  border-radius: 10px;
  width: 200px;
  height: 30px;
  margin: 5px auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
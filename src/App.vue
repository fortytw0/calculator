<template>
  <div id="app">

    <div class="container ">
      
      <div class="row justify-content-center">
        <div class="col-8 display my-2">
          {{display_screen_number}}
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row justify-content-center">
        
        <div class="col-8">
          <div class="container">
            <div class="row justify-content-center">
              <Button v-for="number in numbers" :key="number" :numeral="number" @numeral-side="update_display_screen" />
          </div>
        </div>
      </div>

      <div class="col-4">
        <div class="container">
          <div class="row justify-content-center">
            <Operator v-for="operator in operations" :key=operator :operation=operator @operator-side="set_operation" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import "bootstrap/dist/css/bootstrap.min.css"
import "bootstrap"

import Button from '../src/components/Button.vue'
import Operator from '../src/components/Operators.vue'

export default {
  name: 'App',
  components: {
    Button,
    Operator
  },

  data(){
    return {
      numbers : ['1','2','3','4','5','6','7','8','9','Bsp','0','Res'], 
      operations : ['add', 'sub', 'mul', 'div', 'result'],
      display_screen_number : "",
      calc_stack : 0, 
      operation_in_progress : false,
      operation_stack : null
    }
  }, 

  methods: {


    reset_display(){
      this.display_screen_number = ""
      this.operation_in_progress = false
      this.operation_stack = null

    },

    do_operation(){

      if (this.operation_stack=='add'){
        return String(this.calc_stack + Number(this.display_screen_number))
      }

      else if (this.operation_stack=='sub'){
        return String(this.calc_stack - Number(this.display_screen_number))
      }

      else if (this.operation_stack=='mul'){
        return String(this.calc_stack * Number(this.display_screen_number))
      }

      else {
        if (Number(this.display_screen_number)==0){
          return this.calc_stack
        }
        return String(this.calc_stack / Number(this.display_screen_number))
      }

    },

    set_operation(operator){

      if (operator=="result") {
        this.calc_stack = this.do_operation()
        this.display_screen_number = String(this.calc_stack)
        this.operation_stack = null
        this.operation_in_progress = false
      }

      else {
        if (this.operation_in_progress==true){
          this.calc_stack = this.do_operation()
          this.operation_stack = operator
          this.display_screen_number = ""
        }

        else {
          this.calc_stack = Number(this.display_screen_number)
          this.operation_stack = operator
          this.display_screen_number = ""
          this.operation_in_progress==true
        }

      }


      

    },

    update_display_screen(value){

      
      if (value=='Bsp'){
        this.display_screen_number = this.display_screen_number.substring(0, this.display_screen_number.length - 1);
      }

      else if (value=="Res"){
        this.reset_display()
      }

      else {
        this.display_screen_number += value
      }      
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.mainframe {
  min-height: 480px;
  border-color:#2c3e50;
  border-style: solid;
  border-radius: 0;
}

.display {
  height: 120px;
  border-color:green;
  border-style: solid;
  border-radius: 0;
  font-size: 3em;
}

</style>

<template>
  <button class="col-3 button mt-2" @click="number_clicked">
    {{numeral}}
  </button>
</template>

<script>
export default {

  props:{
    numeral:String
  }, 

  methods: {

    number_clicked(){
      
      this.$emit('numeral-side', this.numeral)
    }

  }

}
</script>



<style scoped>

.button {
  border-color:black;
  border-style: solid;
  border-radius: 0;
  margin: 2px;
  font-size: 2.5em;
}

.button:hover{

  background-color: #ddddff;

}

.button:active {
  background-color:#5555ab ;
}




</style>


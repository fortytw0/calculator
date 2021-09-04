<template>
    <button class="col-12 operations mt-2" @click="operation_clicked">
        {{operation}}
    </button>
</template>


<script>
export default {
    props:{
        operation:String
    },

    methods: {

        operation_clicked (){
            this.$emit("operator-side", this.operation)
        }
    }


}
</script>


<style scoped>

.operations {

  border-color:black;
  border-style: solid;
  border-radius: 0;

  margin: 2px;
  font-size: 2em;
}

.operations:hover{

  background-color: #ddffdd;

}

.operations:active {
  background-color:#6dbd6d ;
}

</style>
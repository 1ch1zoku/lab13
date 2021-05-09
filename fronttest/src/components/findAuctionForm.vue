<template>
      <form  v-on:submit.prevent = "FindAuctionZ" class="newForm" v-if="showFindAuctionForm">
    вид лоту <input type="text" v-model="findAuction.Nameme"> <br>
    ціна <input type="number" v-model.number="findWorker.prise" > <br>
    <button type="submit" >Знайти </button>
    <button type="reset"> Очистити </button>
  </form>
</template>

<script>
export default {
    name:"findAuctionForm", 
    props:{
        modelValue: Object
    },
    data(){
      return {
          showFindAuctionForm: false,
          findAuction: this.modelValue
      } 
    },
    methods:{
        FindauctionZ(){
            this.$emit("update: modelValue", this.findAuction)
            this.hide()
        },
        show(){
            this.showFindAuctionForm=true
        },
        hide(){
            this.showFindAuctionForm=false
        }
    }
}
</script>

<style scoped>
.newForm{
  text-align: left;
  display: inline-block;
   font:14px Arial, Helvetica, sans-serif;
   margin-top: 20px;
}
</style>
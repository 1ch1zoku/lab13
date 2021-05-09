<template>
    <form  v-on:submit.prevent = "addNewAuction" class="newForm" v-if="showNewAuctionForm">
    Назва лоту <input type="text" v-model="newAuction.Name"><br>
    Вид лоту <input type="text" v-model="newAuction.Nameme"> <br>
    Старт торгів <input type="number" v-model.number="newAuction.start"> <br>
    Ціна <input type="number" v-model.number="newAuction.prise" > <br>
    Кінцева ціна <input type="number" v-model.number="newAuction.finish" > <br>
    <button type="submit" >Додати </button>
    <button type="reset"> Очистити </button>
  </form>
</template>

<script>
export default {
    name:"NewAuctionForm", 
    props:{
        modelValue: Object
    },
    data(){
      return {
          showNewAuctionForm: false,
          newAuction: this.modelValue
      } 
    },
    methods:{
        addNewAuction(){
            this.$emit("update: modelValue", this.newAuction)
            this.hide()
        },
        show(){
            this.showNewAuctionForm=true
        },
        hide(){
            this.showNewAuctionForm=false
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
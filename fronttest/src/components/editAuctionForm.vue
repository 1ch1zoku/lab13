<template>
    <form  v-on:submit.prevent = "ueditSelectedAuction" class="newForm" v-if="showEditAuctionForm">
    Назва лоту <input type="text" v-model.lazy="editAuction.Name"><br>
    Вид лоту <input type="text" v-model.lazy="editAuction.Nameme"> <br>
    Старт торгів <input type="number" v-model.number.lazy="editAuction.start"> <br>
    Ціна<input type="number" v-model.number.lazy="editAuction.prise" > <br>
    Кінцева ціна <input type="number" v-model.number.lazy="editAuction.finish" > <br>
    <button type="submit" >Редагувати </button>
    <button type="reset"> Очистити </button>
  </form>
</template>

<script>
export default {
    name:"editWorkerForm", 
    props:{
        modelValue: Object
    },
    data(){
      return {
          showEditAuctionForm: false,
          editAuction: this.modelValue
      } 
    },
    methods:{
        ueditSelectedAuction(){
            this.$emit("update: modelValue", this.editAuction)
            this.hide()
        },
        show(editAuction){
            this.editAuction=editAuction
            this.showEditAuctionForm=true
        },
        hide(){
            this.showEditAuctionForm=false
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
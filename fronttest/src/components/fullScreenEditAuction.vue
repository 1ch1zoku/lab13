<template>
   <form  v-on:submit.prevent = "save">
    Назва лоту  <input type="text" v-model.lazy="editAuction.Name"><br>
    Вид лоту <input type="text" v-model.lazy="editAuction.Nameme"> <br>
    Ставрт аукціону <input type="number" v-model.number.lazy="editAuction.start"> <br>
    Ціна <input type="number" v-model.number.lazy="editAuction.prise" > <br>
    Кінцева ціна <input type="number" v-model.number.lazy="editAuction.finish" > <br>
    <button type="submit" >Редагувати </button>
    <button type="reset"> Очистити </button>
  </form>
</template>

<script>
import storage from '../storage'
export default {
    props: {
        id: String
    },
    data(){
        return{
            editAuction: {}
        }
    },
    mounted(){
        this.editAuction=storage.auction.find(auction => auction.id==Number(this.id))
    },
    method:{
        save(){
            this.$router.push(`/auction/${this.editAuction.id}`);
        }
    }
}
</script>
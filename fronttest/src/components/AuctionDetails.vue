<template>
<div>
<input type="button" value="Редагувати" @click="edit" >
    <ul>
        <li>
      <h3 @click="showDetails">Назва лоту: {{ bk.Name }}</h3>
      <h3>Вид лоту: {{ bk.Nameme }}</h3>
      <h3>Старт аукціону {{ bk.start }}</h3>
      <h3>Ціна {{ bk.prise }}</h3>
      <h3>Кінцева ціна {{ bk.finish }}</h3>
        </li>
    </ul>
</div>
</template>

<script>
import storage from '../storage'
export default {
    props: {
        id: String
    },
    data(){
        return{
            auction: {}
        }
    },
    mounted(){
        this.auction=storage.auction.find(auction => auction.id==Number(this.id))
    },
    method:{
        edit(){
            this.$router.push(`${this.auction.id}/edit`);
        }
    }
}
</script>

<style scoped>
li{
    width: 250px;
    height: 300px;
}
</style>
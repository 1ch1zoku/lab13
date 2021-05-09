<template>
<div class="AuctionTemplate"> 
  <input type="button" value="Додати" v-on:click="showForm" >
  <input type="button" value="Редагувати" v-on:click="showEditForm" >
  <input type="button" value="Видалити" v-on:click="deleteAuction" >
  <input type="button" value="Знайти" v-on:click="showfindAuction" >
  <div class="wrap"> 
    <new-auction-form v-model="newAuction" @submit.prevent="addNewAuction" ref="newAuctionForm"></new-auction-form>
  </div>
  <ul>
    <Auction-template v-for="(b, i) in auction" :key="i" class="Auction" v-on:click="selectAuction(i)" :style="i==selected?'box-shadow: 0 0 20px rgba(0,0,0,0.5);':'' " v-bind:bk="b"></Auction-template>
  </ul>
  <edit-auction-form v-model="editAuction" @submit.prevent="editSelectedAuction" ref="editauctionAuctionForm"></edit-auction-form>
 <find-auction-form v-model="findAuction" @submit.prevent="AuctionZ" ref="findAuctionForm"></find-auction-form>
</div>
</template>

<script>
import AuctionTemplate from './AuctionTemplate.vue';
import NewAuctionForm from './NewAuctionForm.vue';
import findAuctionForm from './findAuctionForm.vue';
import editAuctionForm from './editAuctionForm.vue';
import storage from '../storage';

export default{
    name:"auction", 
    components:{
      AuctionTemplate,
      NewAuctionForm,
      findAuctionForm,
      editAuctionForm,
      
    },
    data(){
      return {
      selected:-1,
      children_count:0,
        auction:storage.auction,
        newAuction: {
          Name: "",
          Nameme:"",
          start: 0,
          prise: 0,
          finish: 0       
        },
        editAuction:{
          Name: "",
          Nameme:"",
          start: 0,
          prise: 0,
          finish: 0       
        },
        findAuction: {
          Nameme "",
          prise: 0
        }
      };
    },
    methods: {
    addNewAuction(){
      console.log(this.newAuction)
      let newAuctionCopy = Object.assign({}, this.newAuction)
      this.auction.push(newAuctionCopy)
      this.showNewAuctionForm = false
    },
    showForm(){
       this.$refs.newAuctionForm.show();
    },
    selectAuction(index){
      this.selected = index;
    }, 
    showEditForm(){
      if (this.selected>=0){
        this.editAuction = this.auction[this.selected];
        this.$refs.editAuctionForm.show(this.editAuction);
      }
      else alert("Виберіть лот")
    },
    editSelecteduAction(){
      this.showEditAuctionForm = false;
    },
    showfindAuction(){
      this.$refs.findAuctionForm.show();
    },
    FindAuctionZ(){
      var p=this.findAuction.position;
      var z=this.findAuction.count_kids;
      this.auction=this.auction.filter(x=>x.position==p && x.count_kids<=z);
      this.showFindAuctionForm=false;
    },
    deleteAuction(){
      if (this.selected>=0)
        this.auction.splice(this.selected, 1);
    }
  },
};
</script>
<style>
body{
  background:url(https://i1.wp.com/hipzmag.com/wp-content/uploads/2018/12/novogodnij-fon-2018.jpg);
  background-size: 100%;
  text-align: center;
}
ul{
  list-style: none;
}
.bookkeeping {
  padding: 50px;
  padding-top: 0px;
}
.newForm{
  text-align: left;
  display: inline-block;
   font:14px Arial, Helvetica, sans-serif;
   margin-top: 20px;
}
input{
  background: linear-gradient(0deg, rgba(255,255,255,0.9026961126247374) 0%, rgba(176,175,174,1) 100%);
}
input[type=button]{
text-align:center; 
 padding:11px 33px;   
 font:18px Arial, Helvetica, sans-serif; 
 font-weight:bold; 
 box-shadow:1px 1px 5px #000000, inset 0px 0px 1px #ffffff;  
 text-shadow: 2px 1px 0px #adabab; 
 }

 input[type=button]:hover{
 padding:15px 40px; 
 font:18px Arial, Helvetica, sans-serif; 
 font-weight:bold; 
 color:#000000; 
 box-shadow:3px 3px 6px #000000, inset 0px 0px 1px #ffffff;  
 text-shadow: 2px 1px 0px #adabab; 
}
li{
    background: linear-gradient(0deg, rgba(255,255,255,0.9026961126247374) 0%, rgba(176,175,174,1) 100%);
    margin: 20px;
    width: 130px;
    display: inline-block;
}
</style>

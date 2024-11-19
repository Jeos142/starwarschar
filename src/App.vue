<template>
  <div class="app">
    <PeopleList
        :peoples="this.peoples"
        v-if="!isLoading"
        @show-vehicle="showVehicle"
    />

    <div v-else class="loading_text">
      Loading...
    </div>
    <transition>
      <div
        class="modal"
        v-if="showModal"
        @click="hideModal"
      >
        <div class="modal-content">
         <VehicleList :garage="this.garage"/>
        </div>
      </div>
    </transition>
    <div class="page__wrapper">
      <div
          v-for="pageNumber in totalPages"
          :key="pageNumber"
          class="page"
          :class="{
            'current-page':page===pageNumber
          }"
          @click="changePage(pageNumber)"
      >
        {{pageNumber}}
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PeopleList from "@/components/PeopleList.vue";
import PeopleListItem from "@/components/PeopleListItem.vue";
import VehicleList from "@/components/VehicleList.vue";
export default {
  components:{
    VehicleList,
    PeopleList,
    PeopleListItem
  },
  data(){
    return{
      peoples: [],
      page:1,
      limit:10,
      isLoading:false,
      totalPages:0,
      showModal:false,
      garage:[],
    }
  },
  methods:{
    async showVehicle(vehicles){
      this.garage=[]
      for(let i=0; i<vehicles.length; i++){
        const response=await axios.get(vehicles[i],);
        this.garage.push(response.data);

      }
      this.showModal=true;
    },
    hideModal(){
      this.showModal=false;
    },
    changePage(pageNumber){
      this.page=pageNumber;
      this.fetchPeople()
    },
    async fetchPeople(){
      try{
        this.isLoading=true
        const query='https://swapi.dev/api/people/?page='+String(this.page)
        const response = await axios.get(query,);
        this.totalPages=Math.ceil( response.data.count/this.limit);

        console.log(response.data.results);
        this.peoples = response.data.results;

      }
    catch (e){
      alert("Error fetching People");
    } finally {
        this.isLoading=false
      }

    },
  },
  mounted() {
    this.fetchPeople();
  }
}
</script>

<style >
@import url(https://fonts.googleapis.com/css?family=Droid+Sans:400,700);
@font-face {
  font-family: "SW";
  src: url("./fonts/STARWARS.woff") format('woff');
}
  *{
    margin: 0;
  }
  .app{
    font-family: "Droid Sans", arial, verdana, sans-serif;
    color: #ff6;
    font-size: 25px;
    text-shadow: 1px 1px 2px red, 0 0 1em teal, 0 0 0.2em teal;
    background-image: url("https://pibig.info/uploads/posts/2022-11/1669807082_1-pibig-info-p-chernii-kosmos-vkontakte-1.jpg");
    background-color: #000;

    min-height: 100vh;
  }
  .loading_text{
    display: flex;
    justify-content: center;
    font-size: 100px;

  }
  h1{

    font-family: "SW", verdana, sans-serif;
    font-size: 50px;
    text-align: center;
  }
  strong{
    font-family: "SW", verdana, sans-serif;
  }
  .modal{
    top:0;
    left:0;
    right:0;
    bottom:0;
    background:  rgba(0,0,0,0.5);
    position: fixed;
    display: flex;
    animation: 0.3s alternate ease;
  }
  .modal-content{
    margin:auto;
    background: black;
    min-height: 50px;
    min-width: 300px;
    padding: 20px;
    border-radius: 10px;
    border: 5px solid teal;
    box-shadow: 1px 1px 10px 10px  #3ab09e;

  }
  .page__wrapper{
    display: flex;
    margin-top: 40px;
    justify-content: center
  }
  .page{
    border: 1px solid teal;
    padding: 10px;
    margin-left: 5px;
    cursor: pointer;
  }
  .current-page{
    border: 2px solid gold;
  }
  .v-enter-active,
  .v-leave-active {
  transition: opacity 0.5s ease;
  }

  .v-enter-from,
  .v-leave-to {
  opacity: 0;
  }
</style>
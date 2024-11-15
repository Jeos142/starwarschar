<template>
  <div v-if="peoples.length>0" style="padding-top: 20px">
    <h1> Character list</h1>
    <transition-group name="user-list">
      <people-list-item :people="this.emptyArray" style="font-family: SW; text-decoration:underline; border: 2px solid gold; border-radius: 10px" />
      <PeopleListItem
          v-for="people in peoples"
          :people="people"
          @show-vehicle="$emit('show-vehicle',people.vehicles)"
      />


    </transition-group>

  </div>
  <h2 v-else style="color:red"> List is empty</h2>
</template>

<script>
import PeopleListItem from "@/components/PeopleListItem";
export default {
  components:{PeopleListItem},
props:{
    peoples:{
      type: Array,
      required: true
    }
  },
  data(){
    return{
      emptyArray:{
        name:"Name:",
        height:"Height:",
        mass:"Weight:",
        hair_color:"Hair color:",
        skin_color:"Skin color:",
        vehicles:"Vehicle:"
      },
    }
  }
}
</script>

<style  scoped>

</style>
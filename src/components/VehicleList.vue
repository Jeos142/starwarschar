<template>
  <div v-if="garage.length>0">
    <vehicle-list-item
        v-for="garageItem in garage"
        :garage-item="garageItem"
    />
  </div>
  <div v-else style="font-size: 40px; display: flex; justify-content: center;">No vehicle</div>
</template>

<script>
import VehicleListItem from "@/components/VehicleListItem.vue";
export default {
  components:{VehicleListItem},
  props:{
    garage:{
      type: Array,
      required: true
    }
  }
}
</script>

<style  scoped>

</style>
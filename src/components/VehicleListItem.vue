<template>
  <div class="post">
    <div class="properties"> <strong>Name:  </strong>{{garageItem.name}}</div>
    <div class="properties"> <strong>Model:  </strong>{{garageItem.model}} </div>
    <div class="properties"> <strong>Cost (in credits):  </strong>{{garageItem.cost_in_credits}} </div>
    <div class="properties"> <strong>Crew:  </strong>{{garageItem.crew}} </div>
    <div class="properties"> <strong>Passengers:  </strong>{{garageItem.passengers}} </div>
  </div>
</template>

<script>
export default {
  props:{
    garageItem:{
      type: Object,
      required: true
    }
  }
}
</script>

<style  scoped>
.post{
  padding: 15px;
  border: 2px solid teal;
  margin-top:15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.properties{

  min-width: 20%;

}
</style>
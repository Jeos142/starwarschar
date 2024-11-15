<template>
  <div class="post">
    <div class="properties"> {{people.name}}</div>
    <div class="properties"> {{people.height}}</div>
    <div class="properties"> {{people.mass}}</div>
    <div class="properties"> {{people.hair_color}}</div>
    <div class="properties" > {{people.skin_color}}</div>
    <div  @click="$emit('show-vehicle',people.vehicles)"><strong style="cursor:pointer">Vehicle</strong></div>
  </div>
</template>

<script>
export default {
  props:{
    people:{
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.post{
  padding: 15px;
  border: 2px solid teal;
  margin-top:15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.properties{
  min-width: 16%;
}
</style>
<template>
<div>
  <h1>Your Itineraries</h1>
  <div class="form"><create-itinerary /></div>
  <div class = "itineraries"><itineraries /></div>
  
</div>
  
</template>

<script>
import CreateItinerary from '../components/CreateItinerary.vue'
import Itineraries from '../components/Itineraries.vue'
export default {
  components: { Itineraries, CreateItinerary },

}
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@200&display=swap");
h1 {
  margin-top:30px;
  text-align: center;
  font-size: 3rem;
  /* font-weight: bold; */
  color:#f03768;
  text-shadow: 0px 0px 12px #ff006a;
  font-family: "Roboto Mono";
}
.form {
  text-align: center;
  margin-bottom: -45px;
}


</style>
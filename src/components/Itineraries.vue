<template>
<body>
  

  <div class="wrapper">
    <div class="gotoButton"><router-link style="text-decoration: none; color: inherit;" v-bind:to="{ name: 'landmark-search' }"
              ><button class="landmarkLink">Go To Landmarks</button></router-link></div>
            <br>
    <div
      class="wrap-1"
      v-for="(itinerary, index) in itineraries"
      v-bind:key="itinerary.itineraryId"
    >
      <!-- <button
        class="delete"
        v-on:click.prevent="deleteItinerary(itinerary.itineraryId)"
      >
        Delete Itinerary
      </button> -->
      <button class = "delete">
    <svg v-on:click.prevent="deleteItinerary(itinerary.itineraryId)" xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
  <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
  <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
</svg>
<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-printer" viewBox="0 0 16 16">
  <path d="M2.5 8a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1z"/>
  <path d="M5 1a2 2 0 0 0-2 2v2H2a2 2 0 0 0-2 2v3a2 2 0 0 0 2 2h1v1a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2v-1h1a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2h-1V3a2 2 0 0 0-2-2H5zM4 3a1 1 0 0 1 1-1h6a1 1 0 0 1 1 1v2H4V3zm1 5a2 2 0 0 0-2 2v1H2a1 1 0 0 1-1-1V7a1 1 0 0 1 1-1h12a1 1 0 0 1 1 1v3a1 1 0 0 1-1 1h-1v-1a2 2 0 0 0-2-2H5zm7 2v3a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1v-3a1 1 0 0 1 1-1h6a1 1 0 0 1 1 1z"/>
</svg>
</button>
      <input type="radio" :id="itinerary.itineraryId" :value="itinerary.itineraryName" v-model="selected" name="selected" />
      <label :for="itinerary.itineraryId"
        ><div>{{ itinerary.itineraryName }}</div>
        <div class="cross"></div
      ></label>
      <div class=content>
        <div id="startHeader">
          Starting Location:
        </div>
        <div id="startLocation">{{ itinerary.itineraryStart }}</div>
        
        <p id="listHeader">Points of Interest:</p>
        <div v-for="(landmark, index2) in landmarkNames" v-bind:key="landmark">
          <div id="landmarks" v-if="hasLandmark(index2, index)" >{{ landmark }}<svg v-on:click="removeFromItinerary(index, index2)" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-circle" viewBox="0 0 16 16">
  <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
  <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
</svg></div>
          
        </div>
        <!-- <edit-itinerary /> -->
        <!-- <div>
          <div class="field">
            <label for="landmarkId">Enter Landmark ID </label>
            <input
              name="landmarkId"
              type="text"
              v-model="landmarkList[itinerary.itineraryId]"
            />
          </div>
          <div class="actions">
            <button
              type="submit"
              v-on:click="updateItinerary(itinerary.itineraryId, index)"
            >
              Add Landmark
            </button>
          </div>
        </div> -->
      </div>
    </div>
    
   
  </div>
  </body>
</template>
<script>
// import EditItinerary from "../components/EditItinerary.vue";
import itineraryService from "../services/ItineraryService.js";
export default {
  name: "itineraries",
  // components: { EditItinerary },
  data() {
    return {
      addLandmark: false,
      itineraries: {},
      landmarkList: [],
      selected: -1,

      landmarkNames: [
        "Tokyo National Museum",
        "Ghibli Museum",
        "Sensoji Temple",
        "Ueno Park",
        "Meiji Shrine",
        "Tokyo Skytree",
        "Kabuki-za Theatre",
        "Tsukiji Outer Market",
        "Hachiko Statue",
        "Nakamise-dori Street",
        "Tokyo Disneyland",
        "Harajuku",
        "Shinjuku Gyoen National Garden",
        "Tokyo Dome City",
        "Edo-Tokyo Museum",
        "Mount Mitake",
        "Ryogoku",
        "Tokyo Sea Life Park",
        "Nakano Broadway",
        "Sengakuji Temple",
      ],
    };
  },
  computed: {
    filteredLandmarkList() {
      const filteredList = this.landmarkNames.filter(
        (landmarkId) => landmarkId === this.landmarkNames[0]
      );
      return filteredList;
    },
  },
  created() {
    // itineraryService.getItinerary(2).then((response) => {
    //   this.itinerary = response.data;
    // }),
    console.log("success");
    itineraryService.getAllItineraries().then((response) => {
      this.itineraries = response.data;
    });
  },
  methods: {
    deleteItinerary(id) {
      itineraryService.deleteItinerary(id).then((response) => {
        console.log(response);
        this.$router.go();
      });
    },
    updateItinerary(id, i) {
      this.addLandmark = true;
      var input = this.itineraries[i].landmarkList + "," + this.landmarkList;
      var splitted = input.split(",");
      var collector = {};
      for (let i = 0; i < splitted.length; i++) {
        key = splitted[i].replace(/^\s*/, "").replace(/\s*$/, "");
        collector[key] = true;
      }
      var out = [];
      for (var key in collector) {
        out.push(key);
      }
      var output = out.join(",");
      const itinerary = {
        landmarkList: "," + output,
      };
      itineraryService.updateItinerary(id, itinerary).then((response) => {
        console.log(response);
        this.$router.go();
      });
    },
    hasLandmark(id, i) {
      if (this.itineraries[i].landmarkList == null) {
        return false;
      }
      var landmarks = this.itineraries[i].landmarkList;
      console.log(landmarks);
      return landmarks.includes("," + id + ",");
    },

  removeFromItinerary(id, i) {
      this.addLandmark = true;
      console.log(i);
      console.log(id);
      var input = this.itineraries[id].landmarkList;
      var splitted = input.split(",");
      var collector = {};
      for (let i = 0; i < splitted.length; i++) {
        key = splitted[i].replace(/^\s*/, "").replace(/\s*$/, "");
        collector[key] = true;
      }
      console.log(collector);
      var out = [];

      for (var key in collector) {
        out.push(key);
      }
      out = out.filter(num => {
        return num != i;
      });
      
      var output = out.join(",");
      console.log(output);
      const itinerary = {
        landmarkList: "," + output,
      };
      itineraryService.updateItinerary(this.itineraries[id].itineraryId, itinerary).then((response) => {
        console.log(response);
        this.$router.go();
      });
    },
  },

};
</script>
<style scoped>
.gotoButton{
  display: flex;
  justify-content: center;
}
svg{
  cursor: pointer;
}
#landmarks{
  color:white;
}
.wrap-1{
  padding-bottom: 20px;
}
.delete {
  background: none;
  border: none;
  
  cursor: pointer;
}
.itinerarylist {
  margin-left: 40px;
}
tr:nth-child(odd) {
  background-color: rgb(238, 238, 238);
}
tr:nth-child(even) {
  background-color: rgb(255, 255, 255);
}
.itinerary {
  padding: 15px;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  /* font-family: 'Space Mono', monospace; */
  color: #fccaff;
}

body {
   min-height: 200vh;
  background-color: #07163a;
}

.wrapper {
  max-width: 800px;
  width: 100%;
  margin: 10vh auto;
  
}

/* h1 {
  font-size: 2em;
  margin-bottom: 20px;
  text-align: center;
} */

input {
  display: none;
}

label {
  display: flex;
  width: 100%;
  height: 50px;
  cursor: pointer;
  border: 3px solid #fccaff;
  user-select: none;
}

label div:first-child {
  width: 100%;
  line-height: 45px;
  margin-left: 10px;
  font-size: 2em;
  

}

.cross {
  margin-right: 15px;
  margin-top: 3px;
}

.cross:before,
.cross:after {
  content: "";
  border-top: 2px solid #fccaff;
  width: 15px;
  display: block;
  margin-top: 18px;
  transition: 0.3s;
}

.cross:after {
  transform: rotate(90deg);
  margin-top: -2px;
}

.content {
  box-sizing: border-box;
  font-size: 1.5em;
  margin: 10px 10px;
  max-height: 0;
  overflow: hidden;
  transition: max-height, 0.5s;
}
#listHeader{
  font-weight: bold;
  color:#f03768
}

input:checked ~ .content {
  max-height: 800px;
  transition: max-height, 1s;
}

input:checked ~ label .cross:before {
  transform: rotate(180deg);
}

input:checked ~ label .cross:after {
  transform: rotate(0deg);
}

.questions {
  margin-top: 20px;
  max-height: 0;
  overflow: hidden;
  transition: max-height, 0.5s;
}

.questions label {
  border: none;
  box-shadow: none;
  margin: 0;
}

input:checked ~ .questions {
  max-height: 400px;
  border-bottom: 2px solid #3e474f;
  transition: 1s;
}

/*----------tool-tip------------*/

.tip {
  color: #f03768;
  cursor: help;
  position: relative;
  overflow: visible;
  /* font-family: monospace; */
  font-size: 1.3em;
}

.tip:before,
.tip:after {
  position: absolute;
  opacity: 0;
  z-index: -100;
  transform: translateY(-30%);
  transition: 0.4s;
}

.tip:before {
  content: "";
  border-style: solid;
  border-width: 0.8em 0.5em 0 0.5em;
  border-color: #fccaff transparent transparent transparent;
  transform: translateY(-200%);
  bottom: 90%;
  left: 50%;
}

.tip:after {
  content: attr(data-tip);
  background: #3e474f;
  color: white;
  width: 150px;
  padding: 10px;
  font-size: 0.8em;
  bottom: 150%;
  left: -50%;
}

.tip:hover:before,
.tip:hover:after {
  opacity: 1;
  z-index: 100;
  transform: scaleY(1);
}
.landmarkLink {

  color:rgb(104, 104, 255);
  text-shadow: 0px 0px 15px rgb(57, 57, 255);
  background: none;
  border: none;
  font-size: 1.5rem;
}
.landmarkLink:hover{
  color: rgb(253, 197, 234);
  /* text-decoration-color: rgb(255, 240, 250); */
  text-shadow: 0px 0px 15px rgb(255, 57, 255);
  transition: .4s;
  text-decoration: none;
}
router-link:hover{
  text-decoration: none;
}
svg{
  margin-left: 8px;
}
#startHeader{
  font-weight: bold;
  color:#f03768
}
#startLocation{
  color: white;
  margin-bottom: 18px;
}
</style>
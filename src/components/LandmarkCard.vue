!<template>
  <div id="landmarkCard" func: this.updateLandmarks> 
    <!-- <button @click="updateLandmarks">Update Landmarks</button>  -->
    <!-- <div>
      <h2>Find Landmarks</h2>
      <label >Input your desired search radius: 
        <input
          class="form-control search_radius mb-4"
          v-model="radius"
          type="number"
          placeholder="search radius"
        />
        Please input your starting location.

         <gmap-autocomplete placeholder="Starting Location" @place_changed="initMarker"></gmap-autocomplete>
        <button @click="setStartingLocation">Set</button> 
        <p>Current starting location is: {{startLocationName}} </p>
      </label>
      <br />
    </div> -->
    
    <div class="center">
      
      <div v-for='(landmark) in landmarks' v-bind:key="landmark.id" class="property-card">
        <a v-bind:href="'/landmarks/' + landmark.landmarkId">
          <div class="property-image" v-bind:style="'background-image:url(' + landmark.photoUrl + ')'">
            <div class="property-image-title"></div></div
        ></a>
        <a v-bind:href="'/landmarks/' + landmark.landmarkId">
        <div class="property-description">
          <h5>{{landmark.name}}</h5>
          <p>
            {{landmark.description}}
          </p>
        </div>
        </a>
        <a v-bind:href="'/' + landmark.landmarkId">
          <div class="property-social-icons"></div>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import landmarkService from "../services/LandmarkService.js";
import photoService from "../services/PhotoService.js";

export default {
    name:'landmark-card',
    methods: {
      updateLandmarks() {
        console.log("Update Landmarks", this.landmarks);
        for(let i = 0; i < this.landmarks.length; i ++) {
          this.$set(this.landmarks[i], 'photoUrl', this.photos[i].photoUrl);
          // this.$set(this.landmarks[i], 'location', this.locationMarkers[i].position)
        }
      
      },
    setStartingLocation() {
      if (this.existingPlace) {
        //Grabs the lat and lng of the entered address. 
        this.startLocation = {
          lat: this.existingPlace.geometry.location.lat(),
          lng: this.existingPlace.geometry.location.lng(),
        };
        //Centers map on starting position
        this.center = this.startLocation;
        //Set the starting location text
        this.startLocationName = this.existingPlace.formatted_address;
      }
    }
    },
    data() {
        return {
            idFilter: "",
            landmarks: [],
            photos: [],
            filteredPhotos: [],
            locationMarkers: [],
            radius: 5000,
            startLocation: {
       
            },
            startLocationName: 'Not selected'
            };
    },

    created() {
        photoService.search().then((response) => {
        this.photos = response.data;
          this.updateLandmarks();
        });
        landmarkService.search().then((response) => {
        this.landmarks = response.data;
          this.updateLandmarks();
        });
        


        //Hardcoded Coordinates
        const chureitoPagoda = {
          lat: 35.5012626,
          lng: 138.8013852,
        };
        const ghibli = {
          lat: 35.696238,
          lng: 139.5704317,
        };
        const fushimiInariShrine = {
          lat: 34.9671402,
          lng: 135.7726717,
        };
        const tokyoNatMuseum = {
          lat: 35.7188351,
          lng: 139.7765215,
        };
        const univStudioJapan = {
          lat: 34.6691514,
          lng: 135.4327486,
        };

        
        this.locationMarkers.push({ position: chureitoPagoda });
        this.locationMarkers.push({ position: ghibli });
        this.locationMarkers.push({ position: fushimiInariShrine });
        this.locationMarkers.push({ position: tokyoNatMuseum });
        this.locationMarkers.push({ position: univStudioJapan });

        







    },
    beforeMount () {
      this.updateLandmarks();
    }
    
    




};
</script>

<style scoped>
#landmarkCard{
  background-color: #07163a;
  min-height: 500vh;
}
body {
  background-color: #f2f2f2;
  font-family: "RobotoDraft", "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
}

* {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

h5 {
  color: pink;
  margin: 0px;
  font-size: 1.3em;
  font-weight: 1200;
  background-color:#4d4c4c;
  border-radius: 6px;
  padding-top: 5px;
  padding-bottom: 5px;
  margin-bottom: 5px;
}

p {
  font-size: 1em;
}

.center {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  align-items: center;
  margin-left: 200px;
  padding-right: 200px;
}

/* End Non-Essential */

.property-card {
  height: 36em;
  width: 28em;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  position: relative;
  margin-bottom: 50px;
  margin-right: 80px;

  -webkit-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  -o-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  border-radius: 4px;
  overflow: hidden;
  -webkit-box-shadow: 15px 15px 27px #363636;
  box-shadow: 15px 15px 27px #363636;
}
/* ^-- The margin bottom is necessary for the drop shadow otherwise it gets clipped in certain cases. */

/* Top Half of card, image. */

.property-image {
  height: 20em;
  width: 30em;
  /*padding: -1em 2em; */
  position: Absolute;
  margin-left: -24px;
  top: 0px;
  /* -webkit-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  -o-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  transition: all 0.9s cubic-bezier(0.645, 0.045, 0.355, 1); */
  background-image: url("https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Tokyo_National_Museum%2C_Honkan_2010.jpg/1200px-Tokyo_National_Museum%2C_Honkan_2010.jpg");
  background-size: cover;
  background-repeat: no-repeat;
}

/* Bottom Card Section */

.property-description {
  background-color: #fafafc;
  height: 18em;
  width: 28em;
  position: absolute;
  bottom: 0em;
  /* -webkit-transition: all 0.8s cubic-bezier(0.645, 0.045, 0.355, 1);
  -o-transition: all 0.8s cubic-bezier(0.645, 0.045, 0.355, 1);
  transition: all 0.8s cubic-bezier(0.645, 0.045, 0.355, 1); */
  padding: 0.5em 1em;
  text-align: center;
}

/* Social Icons */

/* .property-social-icons {
  width: 1em;
  height: 1em;
  background-color: black;
  position: absolute;
  bottom: 1em;
  left: 1em;
  /* -webkit-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  -o-transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1);
  transition: all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1); */
/* } */ 

/* Property Cards Hover States */

/* .property-card:hover .property-description {
  height: 0em;
  padding: 0px 1em;
}
.property-card:hover .property-image {
  margin-left: -220px;
  height: 36em;
  width: 50em;
   */
  

/* } */

/* .property-card:hover .property-social-icons {
  background-color: white;
}

.property-card:hover .property-social-icons:hover {
  background-color: blue;
  cursor: pointer;
} */



/* .property-image-title
{
text-align:center;
position:Relative;
top:30%;
opacity:0;
transition:all 0.4s cubic-bezier(0.645, 0.045, 0.355, 1) 0.2s;
color:black;
font-size:1.2em;
} */

/* .property-card:hover .property-image-title
{
opacity:1;
} */
a {
    color: black;
    text-decoration: none;
}

a:hover {
    color:black; 
    text-decoration:none; 
    cursor:pointer;  
}

</style>

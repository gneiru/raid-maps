<script>

export default {
  data() {
    return {
      roomNum: "1001",
      joinCMD: '/join ',
      maps: {
        daily:["ultraezrajal", "ultrawarden", "ultraengineer", "ultratyndarius"],
        weekly: ["ultradrago", "ultranulgath", "championdrakath", "ultradage", "ultradarkon"],
        va: ["thevoid", "icestormarena", "hydrachallenge", "chaoskraken", "ancienttrigoras", "gravechallenge"]
      },
      show: {
        daily: true,
        weekly: true,
        va: false
      }
    }
  },
  methods: {
      async copy(s) {
        await navigator.clipboard.writeText(s);
      }
    },
}
</script>

<template>
  <div class="myInput-group" style="margin-bottom: 30px;">
    <div class="flex flex-cols-3 gap-4">
      <div>
        <label class="label">Room Number</label>
        <input autocomplete="off" class="myInput shrink" type="number" v-model="roomNum">
      </div>
      <div class="flex-cols-1 p-5">
        <div>
          <input type="checkbox" id="daily" value="false" v-model="show.daily" />
          <label for="daily" class="p-2">Daily</label>
        </div>
        <div>
          <input type="checkbox" id="weekly" value="false" v-model="show.weekly" />
          <label for="weekly" class="p-2">Weekly</label>
        </div>
        <div>
          <input type="checkbox" id="va" value="true" v-model="show.va" />
          <label for="va" class="p-2">Void Aura</label>
        </div>
      </div>
    </div>
  </div>
  
  <div class="flex flex-row gap-4">

    <div class="flex-auto" v-show="show.daily === true">
      <strong>Daily Ultras </strong>
      <div v-for="map in maps.daily" class="map">
        <button class="button" @click.stop.prevent="copyTestingCode"> Copy </button>
        {{joinCMD}}{{map}}-{{roomNum}}
      </div>
    </div>

    <div class="flex-auto" v-show="show.weekly === true">
      <strong>Weekly Ultras </strong>
      <div v-for="map in maps.weekly" class="map">
        <button class="button" @click.stop.prevent="copyTestingCode"> Copy </button>
        {{joinCMD}}{{map}}-{{roomNum}}
      </div>
    </div>

    <div class="flex-auto" v-show="show.va === true">
      <strong>Daily VAs</strong> 
      <div v-for="map in maps.va" class="map">
        <button class="button" @click.stop.prevent="copyTestingCode"> Copy </button>
        {{joinCMD}}{{map}}-{{roomNum}}
      </div>
    </div>
  </div>
  
</template>

<style scoped>
/* Room number input */
.myInput {
  max-width: 190px;
  height: 44px;
  background:none;
  border-radius: .5rem;
  padding: 0 1rem;
  border: 2px solid transparent;
  font-size: 1rem;
  border-color: black;
  transition: border-color .3s cubic-bezier(.25,.01,.25,1) 0s, color .3s cubic-bezier(.25,.01,.25,1) 0s,background .2s cubic-bezier(.25,.01,.25,1) 0s;
}

.myInput {
  display: block;
  margin-bottom: .3rem;
  font-size: .9rem;
  font-weight: bold;
  color: #fff;
  transition: color .3s cubic-bezier(.25,.01,.25,1) 0s;
}

.myInput:hover, .myInput:focus, .myInput-group:hover .myInput {
  outline: none;
  border-color: #fff;
  color: #000;
}
.myInput:active{
  width: auto;
}


/* Copy Button */
.button {
  padding: 4px 10px;
  font-size: 17px;
  background: transparent;
  border: none;
  position: relative;
  color: white;
  z-index: 1;
 }
 
 .button::after,
  .button::before {
  content: '';
  position: absolute;
  bottom: 0;
  right: 0;
  z-index: -99999;
  transition: all .4s;
 }
 
 .button::before {
  transform: translate(0%, 0%);
  width: 100%;
  height: 100%;
  background: #49443C;
  border-radius: 50px;
 }
 
 .button::after {
  transform: translate(0px, 0px);
  width: 10px;
  height: 10px;
  background: #615110;
  backdrop-filter: blur(5px);
  border-radius: 50px;
 }
 
 .button:hover::before {
  transform: translate(5%, 20%);
  width: 10px;
  height: 10px;
 }
 
 .button:hover::after {
  border-radius: 50px;
  transform: translate(0, 0);
  width: 100%;
  height: 100%;
 }
 
 .button:active::after {
  transition: 0s;
  transform: translate(-20%, 0%);
 }

/* MAPS STYLE */
.map {
  border-color: #000;
  margin-bottom: 2px;
}

</style>

<script>

export default {
  data() {
    return {
      roomNum: '1001',
      joinCMD: '/join ',
      buttons: [],
      maps: {
        daily:["ultraezrajal", "ultrawarden", "ultraengineer", "ultratyndarius"],
        weekly: ["ultradrago", "ultranulgath", "championdrakath", "ultradage", "ultradarkon"],
        va: ["shadowfall","voidflibbi", "icestormarena", "hydrachallenge", "chaoskraken", "ancienttrigoras", "gravechallenge"]
      },
      show: {
        daily: true,
        weekly: false,
        va: true
      }
    }
  },
  methods: {
    copy(map) {
        const el = document.createElement('textarea');  
        el.value = this.joinCMD + map + "-" + this.roomNum;                                 
        el.setAttribute('readonly', '');                
        el.style.position = 'absolute';                     
        el.style.left = '-9999px';                      
        document.body.appendChild(el);                  
        const selected =  document.getSelection().rangeCount > 0  ? document.getSelection().getRangeAt(0) : false;                                    
        el.select();                                    
        document.execCommand('copy');                 
        document.body.removeChild(el);                  
        if (selected) {                                 
          document.getSelection().removeAllRanges();    
          document.getSelection().addRange(selected);   
        }
    },
    updateButtonInnerText(button) {
      // Get the width and height of the button
      var buttonWidth = button.offsetWidth;
      var buttonHeight = button.offsetHeight;

      // Update the inner text of the button to a check icon
      var checkIcon = document.createElement('i');
      checkIcon.className = 'fas fa-check';
      button.innerHTML = '';
      button.appendChild(checkIcon);

      // Set the width and height of the button
      button.style.width = buttonWidth + 'px';
      button.style.height = buttonHeight + 'px';

      // Reset the inner text of all the buttons in the array
      this.buttons.forEach(b => {
        if (b !== button) {
          b.innerText = 'Copy';
        }
      });
    

    // Add the clicked button to the array of buttons
    this.buttons.push(button);

    }
  }
}

</script>

<template>
  <div class="font-mono mb-4 text-5xl">Daily / Weekly Maps</div>
  <div class="myInput-group" style="margin-bottom: 30px;">
    <div class="flex flex-cols-3 gap-4">
      <div>
        <label class="label">Room Number</label>
        <input autocomplete="off" class="myInput shrink" type="number" v-model="roomNum" >    
      </div>
      <div class="flex-cols-1 p-5">
        <div>
          <input type="checkbox" id="daily" value="false" v-model="show.daily" class="cont"/>
          <label for="daily" class="p-2">Daily</label>
        </div>
        <div>
          <input type="checkbox" id="weekly" value="false" v-model="show.weekly" class="cont" />
          <label for="weekly" class="p-2">Weekly</label>
        </div>
        <div>
          <input type="checkbox" id="va" value="true" v-model="show.va" class="cont"/>
          <label for="va" class="p-2">Void Aura</label>
        </div>
      </div>
    </div>
  </div>
  
  <div class="flex flex-row gap-4">
    <div class="flex-auto" v-show="show.daily === true">
      <strong>Daily Ultras </strong>
      <div v-for="map in maps.daily" class="map">
        <button class="button" @click="copy(map); updateButtonInnerText($event.target)"> Copy </button>
        {{joinCMD}}<strong>{{map}}</strong>-{{roomNum}}
      </div>
    </div>

    <div class="flex-auto" v-show="show.weekly === true">
      <strong>Weekly Ultras </strong>
      <div v-for="map in maps.weekly" class="map">
        <button class="button" @click="copy(map); updateButtonInnerText($event.target)"> Copy </button>
        {{joinCMD}}<strong>{{map}}</strong>-{{roomNum}}
      </div>
    </div>

    <div class="flex-auto" v-show="show.va === true">
      <strong>Daily VAs</strong> 
      <div v-for="map in maps.va" class="map">
        <button class="button" @click="copy(map); updateButtonInnerText($event.target)"> Copy </button>
        {{joinCMD}}<strong>{{map}}</strong>-{{roomNum}}
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
  border-color: #ffb38a;
  transition: border-color .3s cubic-bezier(.25,.01,.25,1) 0s, color .3s cubic-bezier(.25,.01,.25,1) 0s,background .2s cubic-bezier(.25,.01,.25,1) 0s;
}

.myInput {
  display: block;
  margin-bottom: .3rem;
  font-size: .9rem;
  font-weight: bold;
  color: #ff9248;
  transition: color .3s cubic-bezier(.25,.01,.25,1) 0s;
}

.myInput:hover, .myInput:focus, .myInput-group:hover .myInput {
  outline: none;
  border-color: #ff6700;
  color: #1A4D2E;
}
.myInput:active{
  width: auto;
}


/* Copy Button */
.button {
  padding: 4px 10px;
  font-size: 17px;
  font-weight: bold;
  background: transparent;
  border: none;
  position: relative;
  color:#000;
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
  background: #ff6700;
  border-radius: 50px;
 }
 
 .button::after {
  transform: translate(0px, 0px);
  width: 10px;
  height: 10px;
  background: #ff9248;
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
  margin-bottom: 2px;
  color: #ff9248;
}
</style>

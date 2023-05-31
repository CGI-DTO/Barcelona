<template>
  <div id="instruments-menu">
    <div class="container vertical-center">

      <!-- OBSEA Buoy button-->
      <button @click="buoyButtonClicked" :title="$i18n.t('buoyButtonTitle')">
        <svg class="icon-svg" xmlns="http://www.w3.org/2000/svg" width="45" height="45" viewBox="0 0 512 512">
          <path id="Buoy" class="buoyLine"
            d="M237,160c-4.781-7.974-18.144-13.452-23-33-3.366-13.548-1.7-27.055,15-40a39.736,39.736,0,0,1,50,1c14.183,12.3,17.286,32.33,11,46-5.926,12.889-17.827,18.351-21,25-3.9,8.181,40.372,107.418,41,125,0.493,13.813-35.64,91.562-46.12,137.363C257.718,448.292,255.352,444.976,250,445c-4.892.022-7.635,7.094-12.936-13.772C223,375.878,189.094,301.389,189,285,188.868,261.924,242.694,169.5,237,160Z" />
          <path id="SeaSurface" class="seaLine"
            d="M0,265c0.747,0.276,26.493,59.805,50,59,25.725-.881,62.869-58,63-58,0.545,0,46.559,56.567,77,55,29.011-1.493,69.42-57,67-57-2.288,0,46.3,63.112,76,62,28.266-1.058,68.314-61,67-61-0.867,0,41.493,57.342,68,57,24.727-.319,44.789-57.065,44-57" />
        </svg>
      </button>

      
      <!-- FPS button -->
      <button @click="fpsButtonClicked">
        <strong>FPS</strong>
      </button>
      <!-- <button>Config</button> -->

    </div>
  </div>
</template>







<script>


export default {
  name: "InstrumentsMenu",
  created() {
    
  },
  mounted() {
    
  },
  data (){
    return {
      buoyTitle: this.$i18n.t("Wind")
    }
  },
  methods: {
    // USER ACTIONS
    buoyButtonClicked: function(e){
      window.eventBus.emit('InstrumentsMenu_buoyButtonClicked');
    },
    baseButtonClicked: function (e) {
      window.eventBus.emit('InstrumentsMenu_baseButtonClicked');
    },
    // Show/hide FPS panel
    fpsButtonClicked: function(e){
      window.eventBus.emit('InstrumentsMenu_fpsButtonClicked')
    }
  },
  components: {
  }
}
</script>











<style scoped>
.container {
  display: flex;
  flex-direction: column;
  width: fit-content;
  padding:0;
}

.vertical-center {
  margin: 0;
  position: absolute;
  top: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}

/* Button */
button {
  background: #d7effa;
  padding: 4px;
  border: none;
}
button:hover {
  background: #ace1f9;
  border-color: #5fc9f6;
}

/* SVG */
.icon-svg:hover {
  border-radius: 50%;
  background-color: #32bffb;
}


/* OBSEA Buoy SVG style */
.buoyLine, .seaLine {
  fill: none;
  stroke: #1a1a1a;
  stroke-linecap: round;
  stroke-linejoin: bevel;
  stroke-width: 18px;
  fill-rule: evenodd;
}
/* Sea line animation */
.seaLine {
 animation: seaLine 4s alternate infinite ease-in-out; 
}
@keyframes seaLine {
  0% {
    transform: translatex(-20px);
    
  }
  50% {
    transform: translatex(20px);
  }
  100% {
    transform: translatex(-20px);
  }
}

/* Buoy animation */
.buoyLine {
  animation: buoyLine 4s alternate infinite ease-in-out;
  transform-origin: 50% 50%;
}
@keyframes buoyLine {
  0% {
    transform: rotate(10deg);
  }
  50% {
    transform: rotate(-10deg);
  }
  100% {
    transform: rotate(10deg);
  }
}



/* OBSEA Base SVG style */
  .cls-1 {
    fill: #acacac;
  }
  .cls-1, .cls-2, .cls-3, .cls-4, .cls-5, .cls-6 {
    fill-rule: evenodd;
  }
  .cls-2, .cls-4, .cls-5 {
    fill: none;
  }
  .cls-2, .cls-3, .cls-4, .cls-5, .cls-6 {
    stroke: #1a1a1a;
  }
  .cls-2, .cls-3 {
    stroke-width: 18px;
  }
  .cls-3, .cls-6 {
    fill: #1a1a1a;
  }
  .cls-4 {
    stroke-width: 10px;
  }
  .cls-5, .cls-6 {
    stroke-width: 16px;
  }


</style>
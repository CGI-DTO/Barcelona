<template>
  <div id="bottom-section">

    <!-- Bottom icons -->
    <!-- Above water -->
    <div class="bottom-icons" v-show="!isUnderwater">
      <button @click="waveIconClicked" :title="$i18n.t('waveButtonTitle')">
        <svg class="icon-svg" xmlns="http://www.w3.org/2000/svg" width="512" height="512" viewBox="0 0 512 512">
            <path id="Wave" class="svg-wavePath"
              d="M91,345a148.964,148.964,0,0,0,39-34c18.237-22.738,21.847-41.833,31.9-66.57C180.68,198.242,210.248,167.907,225,159c24.989-15.088,68.213-28.479,112-10,45.368,19.146,74.013,67.228,65,79-10.978,14.338-66.772-22.893-88-2-16.914,16.647-8.635,64.768,21,90,17.036,14.5,39.538,20.066,62,18" />
        </svg>
      </button>
      <button @click="windIconClicked" :title="$i18n.t('windButtonTitle')">
        <svg class="icon-svg" xmlns="http://www.w3.org/2000/svg" width="512" height="512" viewBox="0 0 512 512">
          <path id="WindTop" class="svg-windPath"
            d="M117,178c96.486,32.553,201.682,46.769,260,0,20.145-16.156,26.414-30.873,26-41-1.07-26.169-36.825-52.812-63-45-9.183,2.741-23.774,11.71-23,25,0.6,10.338,10.406,20.516,25,23" />
          <path id="WindMiddle" class="svg-windPath"
            d="M64.388,323.7c66.094,22.349,138.154,32.108,178.1,0,13.8-11.092,18.094-21.2,17.81-28.148-0.733-17.966-25.226-36.257-43.155-30.894-6.291,1.882-16.286,8.04-15.756,17.163,0.413,7.1,7.129,14.085,17.126,15.791" />
          <path id="WindBottom" class="svg-windPath"
            d="M149,391c96.486,32.553,201.682,46.769,260,0,20.145-16.156,26.414-30.873,26-41-1.07-26.169-36.825-52.812-63-45-9.183,2.741-23.774,11.71-23,25,0.6,10.338,10.406,20.516,25,23" />
        </svg>

      </button>
    </div>



  </div>
</template>



<script>


export default {
  name:"BottomSection",
  mounted() {
    // Subscribe to camera change to hide OBSEA underwater camera
    window.eventBus.on('Canvas3D_cameraChange', (sceneManager) => {
      let camPos = sceneManager.camera.position;
      if (camPos.y < -10){
        this.isUnderwater = true;
      }
      if (camPos.y > -5)
        this.isUnderwater = false;
    });
  },
  data() {
    return {
      isUnderwater: false,
      showCamera: false,

      showDataBar: true,

      date: new Date(),
      
    }
  },
  methods :{
    waveIconClicked: function() {
      // Open central panel
      // Add information about which panel to open
      window.eventBus.emit('OpenCentralPanel', "seaPanel");
    },
    windIconClicked: function () {
      // Open central panel
      // Add information about which panel to open
      window.eventBus.emit('OpenCentralPanel', "windPanel");
    },
  },
  components: {

  }
}
</script>





<style scoped>
#bottom-section {
  position: absolute;
  bottom: 0px;
  width: 100vw;
  pointer-events: none;
}
.bottom-icons {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  padding: 10px;
  transition: all 0.3s ease;
}

button {
  border-style: none;
  padding: 0;
  margin-bottom: 10px;
  border-radius: 50%;
}


.dataBarButton {
  position: relative;
}
.dataBarButtonOn, .dataBarButtonOn > svg{
  border-bottom-left-radius: 0%;
  border-bottom-right-radius: 0%;
}
.dataBarContainerOn {
  transform: translateY(70px);
}





/* Wave SVG */
.svg-wavePath {
  fill: none;
  stroke: #1a1a1a;
  stroke-width: 20px;
  fill-rule: evenodd;
}

/* Wind SVG */
.svg-windPath {
  fill: none;
  stroke: #1a1a1a;
  stroke-width: 20px;
  fill-rule: evenodd;
}


/* Camera SVG */
.cls-1,
.cls-2 {
  fill: none;
  stroke: #1a1a1a;
  stroke-width: 25px;
}

.cls-2 {
  fill-rule: evenodd;
}


.externalLink1 {
  fill: none;
  stroke-width: 31.35px;
}

.externalLink1,
.externalLink2 {
  stroke: #000;
  stroke-linecap: round;
  stroke-linejoin: round;
  fill-rule: evenodd;
}

.externalLink2 {
  stroke-width: 14.04px;
}
    





/* Meter style */
.meter-1 {
  fill: none;
  stroke-width: 20px;
}

.meter-1,
.meterArrow,
.meter-3 {
  stroke: #1a1a1a;
  fill-rule: evenodd;
}

.meterArrow,
.meter-3 {
  fill: #1a1a1a;
}

.meterArrow {
  stroke-width: 30px;
}

.meter-3 {
  stroke-width: 8px;
}

/* Meter animation */
.meterArrow {
  animation: meterArrow 6s alternate infinite ease-in-out;
  transform-origin: 50% 70%;
}

@keyframes meterArrow {
  0% {
    transform: rotate(20deg);
  }

  50% {
    transform: rotate(-20deg);
  }

  100% {
    transform: rotate(20deg);
  }
}









/* Transitions for elements */
.v-enter-active,
.v-leave-active {
  transition: all 0.3s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
  height: 0;
  transform: translateY(20px);
}
</style>
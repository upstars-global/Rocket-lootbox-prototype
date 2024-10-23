<template>

   <div v-if="loading" class="preloader">
      <img :src="preloader" class="preloader_img" alt="" />
    </div>
  <div class="wrapper">
    
    <div class="rockets_column">
      <div id="rocket_3" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <img :src="liteLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
      </div>
      <div id="rocket_2" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <img :src="liteLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
      </div>
      <div id="rocket_1" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <img :src="liteLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
      </div>
    </div>



      
  </div>
  <img :src="ui_referanse" class="ui_referanse" alt="" />
      <div class="btn_row">
        <img :src="btn1" class="btn_row_btn" alt="" @click="scrollToRocketById('rocket_1')" />
        <img :src="btn2" class="btn_row_btn" alt="" @click="scrollToRocketById('rocket_2')" />
        <img :src="btn3" class="btn_row_btn" alt="" @click="scrollToRocketById('rocket_3')" />
        <img :src="btn4" class="btn_row_btn" alt="" />
      </div>

  
</template>

<script setup lang="ts">
import { ref } from 'vue';

const preloader = ref('src/img/PreloaderAlpa_130x130.svg');
const baseLayer = ref('src/img/Layer_1_for_all_rokets_720x1280.svg');
const liteLayer2 = ref('src/img/1-lite/Layer_2_1-Lite_720x1280.svg');
const liteLayer4 = ref('src/img/1-lite/Layer_4_1-Lite_720x1280.svg'); 
const liteLayer5 = ref('src/img/1-lite/Layer_5_1-Lite_720x1280.svg');
const liteLayer6 = ref('src/img/1-lite/Layer_6_1-Lite_720x1280.svg');
const ui_referanse = ref('src/img/referances/ui_referance.svg');
const btn1 = ref('src/img/referances/btn1.svg');
const btn2 = ref('src/img/referances/btn2.svg');
const btn3 = ref('src/img/referances/btn3.svg');
const btn4 = ref('src/img/referances/btn4.svg');

const loading = ref(true);
const loadedImages = ref(0);
const scrollToRocket = ref<HTMLElement | null>(null);

function scrollToRocketById(rocketId: string) {
  const rocket = document.getElementById(rocketId);
  if (rocket) {
    rocket.scrollIntoView({ behavior: 'smooth' });
    scrollToRocket.value = rocket;
  }
}

function imageLoaded() {
  loadedImages.value++;
  if (loadedImages.value === 4) {
    loading.value = false;
  }
}


</script>


<style scoped>
.rocket_base_layers {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translate(-50%);
  height: 100%;
  width: auto;
}

.wrapper {
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  overflow: hidden;
}

.preloader {
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  background: #000000;
  z-index: 1000;

}

.preloader_img {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 130px;
  width: 130px;
}

.hide {
  opacity: 0;
}

.ui_referanse {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translate(-50%);
  height: 100%;
  width: auto;
  z-index: 100;
}

.btn_row {
  position: absolute;
  height: 7%;
  bottom: 1.5%;
  left: 50%;
  width: 100%;
  transform: translate(-50%);
  display: flex;
  justify-content: space-around;
  max-width: 55vh;
  z-index: 1000;
}

.btn_row_btn {
  height: 100%;
  width: auto;
  position: relative;
  cursor: pointer;
  z-index: 1000;
}


.btn_row_btn:hover {
  filter: brightness(0.8);
}


.rockets_column {
  position: absolute;
  height: 300%;
  width: auto;
  top: 0;
  left: 50%;
  transform: translate(-50%);
  display: flex;
  flex-direction: column;
}

.rocket_container {
  height: 100%;
  width: auto;
  position: relative;
  top: 0;
}
</style>
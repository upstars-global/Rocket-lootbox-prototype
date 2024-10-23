<template>

   <div v-if="loading" class="preloader">
      <img :src="preloader" class="preloader_img" alt="" />
    </div>
  <div class="wrapper">
    
    <div class="rockets_column">
      <div id="rocket_1" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <div id="slot_frame_1" class="slot_frame" :style="{ backgroundImage: `url(${liteLayer3})` }">
        </div>
        <img :src="liteLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="liteLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
      </div>
      <div id="rocket_2" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="proLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <div id="slot_frame_2" class="slot_frame" :style="{ backgroundImage: `url(${proLayer3})` }">
        </div>
        <img :src="proLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="proLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="proLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
      </div>
      <div id="rocket_3" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="maxLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <div id="slot_frame_3" class="slot_frame" :style="{ backgroundImage: `url(${maxLayer3})` }">
        </div>
        <img :src="maxLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="maxLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="maxLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
      </div>
    </div>



      
  </div>
  <img :src="ui_referanse" class="ui_referanse" alt="" />
      <div class="btn_row">
        <img :src="btn1" :class="{'btn_row_btn': true, 'btn_inactive': activeRocket !== 1}" alt="" @click="scrollToRocketById('rocket_1')" />
        <img :src="btn2" :class="{'btn_row_btn': true, 'btn_inactive': activeRocket !== 2}" alt="" @click="scrollToRocketById('rocket_2')" />
        <img :src="btn3" :class="{'btn_row_btn': true, 'btn_inactive': activeRocket !== 3}" alt="" @click="scrollToRocketById('rocket_3')" />
        <img :src="btn4" class="btn_row_btn" @click="scrollToSlotFrame" alt="" />
      </div>

  
</template>

<script setup lang="ts">
import { ref } from 'vue';

const preloader = ref('src/img/PreloaderAlpa_130x130.svg');
const baseLayer = ref('src/img/Layer_1_for_all_rokets_720x1280.svg');
const liteLayer2 = ref('src/img/1-lite/Layer_2_1-Lite_720x1280.svg');
const proLayer2 = ref('src/img/2-Pro/Layer_2_2-Pro_720x1280.svg');
const maxLayer2 = ref('src/img/3-Max/Layer_2_3-Max_720x1280.svg');
const liteLayer3 = ref('src/img/1-lite/Layer_3_1-Lite_258x1656.png');
const proLayer3 = ref('src/img/2-Pro/Layer_3_2-Pro_258x1656.png');
const maxLayer3 = ref('src/img/3-Max/Layer_3_3-Max_258x1656.png');
const liteLayer4 = ref('src/img/1-lite/Layer_4_1-Lite_720x1280.svg');
const proLayer4 = ref('src/img/2-Pro/Layer_4_2-Pro_720x1280.svg');
const maxLayer4 = ref('src/img/3-Max/Layer_4_3-Max_720x1280.svg');
const liteLayer5 = ref('src/img/1-lite/Layer_5_1-Lite_720x1280.svg');
const proLayer5 = ref('src/img/2-Pro/Layer_5_2-Pro_720x1280.svg');
const maxLayer5 = ref('src/img/3-Max/Layer_5_3-Max_720x1280.svg');
const liteLayer6 = ref('src/img/1-lite/Layer_6_1-Lite_720x1280.svg');
const proLayer6 = ref('src/img/2-Pro/Layer_6_2-Pro_720x1280.svg');
const maxLayer6 = ref('src/img/3-Max/Layer_6_3-Max_720x1280.svg');
const ui_referanse = ref('src/img/referances/ui_referance.svg');
const btn1 = ref('src/img/referances/btn1.svg');
const btn2 = ref('src/img/referances/btn2.svg');
const btn3 = ref('src/img/referances/btn3.svg');
const btn4 = ref('src/img/referances/btn4.svg');

const loading = ref(true);
const loadedImages = ref(0);
const scrollToRocket = ref<HTMLElement | null>(null);
const activeRocket = ref(1);

const rockets = ref(['rocket_1', 'rocket_2', 'rocket_3']);
const slotFrames = ref(['slot_frame_1', 'slot_frame_2', 'slot_frame_3']);

function scrollToRocketById(rocketId: string) {
  const rocket = document.getElementById(rocketId);
  if (rocket) {
    rocket.scrollIntoView({ behavior: 'smooth' });
    scrollToRocket.value = rocket;
    activeRocket.value = rockets.value.indexOf(rocketId) + 1;
  }
}

const winSlotFrame = ref(1);
function scrollToSlotFrame() {
  const slotFrameId = slotFrames.value[activeRocket.value - 1];
  const slotFrame = document.getElementById(slotFrameId);
  if (slotFrame) {
    // Добавляем класс slot_frame_acceleration к текущему слот-фрейму
    slotFrame.classList.add('slot_frame_acceleration');

    // Отслеживаем окончание анимации
    slotFrame.addEventListener('animationend', () => {
      // Удаляем класс slot_frame_acceleration
      slotFrame.classList.remove('slot_frame_acceleration');
      
      // Добавляем класс slot_frame_animation_full_speed
      slotFrame.classList.add('slot_frame_full_speed');
      
      // Устанавливаем значение CSS-переменной --background-position-y
      const backgroundPositionY = winSlotFrame.value === 1 ? '900%' : '905%';
      slotFrame.style.setProperty('--background-position-y', backgroundPositionY);
    }, { once: true });
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
  aspect-ratio: 9 / 16;
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


.btn_inactive {
  filter: brightness(0.6);
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
  scroll-behavior: smooth;
}

.rocket_container {
  height: 100%;
  width: auto;
  position: relative;
  top: 0;
}

.slot_frame {
  position: absolute;
  height: 28%;
  top: 37%;
  width: 20vh;
  left: 50%;
  transform: translate(-50%);
  background-size: cover;
  background-position-y: 11%;
  background-repeat: repeat-y;
  border-radius: 10vh;
}

.slot_frame_acceleration {
  animation: slot_frame_animation_acceleration 5s ease-in forwards;
}

@keyframes slot_frame_animation_acceleration {
  100% {
    background-position-y: -500%;
  }
}

.slot_frame_full_speed {
  animation: slot_frame_animation_full_speed 5s linear infinite;
}

@keyframes slot_frame_animation_full_speed {
  100% {
    background-position-y: -700%;
  }
}



.slot_frame_end {
  animation: slot_frame_animation_end 5s ease-out infinite;
}

@keyframes slot_frame_animation_end {
  100% {
    background-position-y: var(--background-position-y);
  }
}



</style>

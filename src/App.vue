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
        <img id="lights_1_waing" :src="liteLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img id="lights_1_spin" :src="liteLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
        <MobileText class="rocket_base_layers" top-text="SPIN AND GET LITE PRIZES" bottom-text="UP TO 1000 AUD" />
      </div>
      <div id="rocket_2" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="proLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <div id="slot_frame_2" class="slot_frame" :style="{ backgroundImage: `url(${proLayer3})` }">
        </div>
        <img :src="proLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img id="lights_2_waing" :src="proLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img id="lights_2_spin" :src="proLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
        <MobileText class="rocket_base_layers" top-text="SPIN AND GET PRO PRIZES" bottom-text="UP TO 2500 AUD" />
      </div>
      <div id="rocket_3" class="rocket_container">
        <img :src="baseLayer" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img :src="maxLayer2" class="rocket_base_layers" alt="" @load="imageLoaded"/> 
        <div id="slot_frame_3" class="slot_frame" :style="{ backgroundImage: `url(${maxLayer3})` }">
        </div>
        <img :src="maxLayer4" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img id="lights_3_waing" :src="maxLayer5" class="rocket_base_layers" alt="" @load="imageLoaded"/>
        <img id="lights_3_spin" :src="maxLayer6" class="rocket_base_layers hide" alt="" @load="imageLoaded"/>
        <MobileText class="rocket_base_layers" top-text="SPIN AND GET MAX PRIZES" bottom-text="UP TO 5000 AUD" />
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
  
  <img id="vinget_layer" :src="vingetLayer7" class="vinget_layer hide" alt="" />
</template>

<script setup lang="ts">
import { ref } from 'vue';
import MobileText from './components/MobileText.vue';

const preloader = ref<string>('src/img/PreloaderAlpa_130x130.svg');
const baseLayer = ref<string>('src/img/Layer_1_for_all_rokets_720x1280.svg');
const liteLayer2 = ref<string>('src/img/1-lite/Layer_2_1-Lite_720x1280.svg');
const proLayer2 = ref<string>('src/img/2-Pro/Layer_2_2-Pro_720x1280.svg');
const maxLayer2 = ref<string>('src/img/3-Max/Layer_2_3-Max_720x1280.svg');
const liteLayer3 = ref<string>('src/img/1-lite/Layer_3_1-Lite_258x1656.png');
const proLayer3 = ref<string>('src/img/2-Pro/Layer_3_2-Pro_258x1656.png');
const maxLayer3 = ref<string>('src/img/3-Max/Layer_3_3-Max_258x1656.png');
const liteLayer4 = ref<string>('src/img/1-lite/Layer_4_1-Lite_720x1280.svg');
const proLayer4 = ref<string>('src/img/2-Pro/Layer_4_2-Pro_720x1280.svg');
const maxLayer4 = ref<string>('src/img/3-Max/Layer_4_3-Max_720x1280.svg');
const liteLayer5 = ref<string>('src/img/1-lite/Layer_5_1-Lite_720x1280.svg');
const proLayer5 = ref<string>('src/img/2-Pro/Layer_5_2-Pro_720x1280.svg');
const maxLayer5 = ref<string>('src/img/3-Max/Layer_5_3-Max_720x1280.svg');
const liteLayer6 = ref<string>('src/img/1-lite/Layer_6_1-Lite_720x1280.svg');
const proLayer6 = ref<string>('src/img/2-Pro/Layer_6_2-Pro_720x1280.svg');
const maxLayer6 = ref<string>('src/img/3-Max/Layer_6_3-Max_720x1280.svg');
const vingetLayer7 = ref<string>('src/img/Layer_7_for_all_rockets_720x1280.svg');
const ui_referanse = ref<string>('src/Ref.svg');
const btn1 = ref<string>('src/img/referances/btn1.svg');
const btn2 = ref<string>('src/img/referances/btn2.svg');
const btn3 = ref<string>('src/img/referances/btn3.svg');
const btn4 = ref<string>('src/img/referances/btn4.svg');


const loading = ref<boolean>(true);
const loadedImages = ref<number>(0);
const activeRocket = ref<number>(1);

const rockets = ref<string[]>(['rocket_1', 'rocket_2', 'rocket_3']);
const slotFrames = ref<string[]>(['slot_frame_1', 'slot_frame_2', 'slot_frame_3']);
const waitingLights = ref<string[]>(['lights_1_waing', 'lights_2_waing', 'lights_3_waing']);
const spinLights = ref<string[]>(['lights_1_spin', 'lights_2_spin', 'lights_3_spin']);

// выиграшный фрейм. Учел что он может быть в начале null поскольку бек еще не отдал значение, 
// тогда слот будет вращаться и проверять значение каждую секунду в function scrollToSlotFrame
const winSlotFrame = ref<number | null>(5);

// массив значений background-position-y для каждого слота, стоит перепроверить. Все версталось за пол дня на очень скорую руку. 
// На мобилке в Хроме может быть смещение из за нижней панели бразера, поэтому возможно стоит использовать фактические значения в пикселях
// либо задать дополнительное значение в dvh для поддерживаемых браузеров
const backgroundPositions = ref<string[]>([
  '-518%',
  '-501%',
  '-486%', 
  '-471%',
  '-453%',
  '-437%',
  '-421%',
  '-405%'
]);

function scrollToRocketById(rocketId: string): void {
  const rocket = document.getElementById(rocketId);
  const vingetLayer = document.getElementById('vinget_layer');

  if (vingetLayer && vingetLayer.classList.contains('fade_in')) {
    vingetLayer.classList.remove('fade_in');
  }

  if (rocket) {
    rocket.scrollIntoView({ behavior: 'smooth' });
    activeRocket.value = rockets.value.indexOf(rocketId) + 1;
  }
}

function scrollToSlotFrame(): void {
  const slotFrameId = slotFrames.value[activeRocket.value - 1];
  const waitingLightId = waitingLights.value[activeRocket.value - 1];
  const spinLightId = spinLights.value[activeRocket.value - 1];
  
  const slotFrame = document.getElementById(slotFrameId);
  const waitingLight = document.getElementById(waitingLightId);
  const spinLight = document.getElementById(spinLightId);
  const vingetLayer = document.getElementById('vinget_layer');

  if (slotFrame && waitingLight && spinLight && vingetLayer) {
    slotFrame.classList.add('slot_frame_acceleration');
    waitingLight.classList.add('fade_out');
    spinLight.classList.add('fade_in');
    vingetLayer.classList.add('fade_in');

    slotFrame.addEventListener('animationend', () => {
      slotFrame.classList.remove('slot_frame_acceleration');
      slotFrame.classList.add('slot_frame_full_speed');
      
      const checkWinSlotFrame = setInterval(() => {
        if (winSlotFrame.value !== null) {
          setSlotFrameStyles(slotFrame, winSlotFrame.value);
          clearInterval(checkWinSlotFrame);
        }
      }, 1000);
    }, { once: true });
  }
}

function setSlotFrameStyles(slotFrame: HTMLElement, winSlotFrameValue: number): void {
  const backgroundPositionY = backgroundPositions.value[winSlotFrameValue - 1] || '-518%';
  slotFrame.style.setProperty('--background-position-y', backgroundPositionY);
  slotFrame.classList.remove('slot_frame_full_speed');
  slotFrame.classList.add('slot_frame_end');
}

function imageLoaded(): void {
  loadedImages.value++;
  if (loadedImages.value === 15) {
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

.vinget_layer {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translate(-50%);
  height: 100%;
  width: auto;
  aspect-ratio: 9 / 16;
  z-index: 50;
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
  z-index: 3000;

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
  animation: slot_frame_animation_acceleration 3s cubic-bezier(1,0,1,1) forwards;
}

@keyframes slot_frame_animation_acceleration {
  100% {
    background-position-y: -250%;
  }
}

.slot_frame_full_speed {
  animation: slot_frame_animation_full_speed 1s linear infinite;
}

@keyframes slot_frame_animation_full_speed {
  100% {
    background-position-y: -250%;
  }
}



.slot_frame_end {
  animation: slot_frame_animation_end 5s cubic-bezier(0,0,0,1) forwards;
}

@keyframes slot_frame_animation_end {
  100% {
    background-position-y: var(--background-position-y);
  }
}


.fade_in {
  animation: fade_in 0.8s ease-in forwards;
}

@keyframes fade_in {
  100% {
    opacity: 1;
  }
}

.fade_out {
  animation: fade_out 0.8s ease-out forwards;
}

@keyframes fade_out {
  0% {
    opacity: 1;
  }
  99% {
    opacity: 0;
    display: block;
  }
  100% {
    display: none;
    opacity: 0;
  }
}


</style>

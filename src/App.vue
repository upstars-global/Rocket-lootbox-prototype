<template>
  <div class="wrapper">
    <img :src="baseLayer" class="rocket_base_layers" alt="" />
    <img :src="liteLayer2" class="rocket_base_layers" alt="" /> 
    <img :src="liteLayer4" class="rocket_base_layers" alt="" />
    <img :src="liteLayer5" class="rocket_base_layers" alt="" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const baseLayer = ref('/src/img/Layer_1_for_all_rokets_720x1280.svg');
const liteLayer2 = ref('/src/img/1-lite/Layer_2_1-Lite_720x1280.svg');
const liteLayer4 = ref('/src/img/1-lite/Layer_4_1-Lite_720x1280.svg'); 
const liteLayer5 = ref('/src/img/1-lite/Layer_5_1-Lite_720x1280.svg');
</script>


<style>
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

body {
  background: #000000;
  margin: 0;
  padding: 0;

}
</style>

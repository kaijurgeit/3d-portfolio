<script setup language="ts">
import { TresCanvas } from '@tresjs/core';
import { Environment, Backdrop, Precipitation } from '@tresjs/cientos';
import Character from './Character.vue';

</script>
<template>
<TresCanvas shadows>
  <!-- @vue-ignore -->
  <TresPerspectiveCamera :args="[75, 16/9, 0.1, 100]" :position="[0, 1.2, 2.0]" :rotation-x="- 10 / 180 * Math.PI "  />
  <Precipitation :count="40" :area="[5, 3, 3]" :size=".02" :speed="-0.1" :position-y="1" :randomness=".5" />
  <!-- <TresGridHelper :args="[10, 10]" :scale=".5" :position="[0, 0.1, 0]" /> -->
  <Environment preset="city" />
  <Suspense>
    <Character :position="[0, 0.02, 0]" cast-shadow />
  </Suspense>
  <Backdrop :floor="100" :segments="10" :position="[0, 0, -3]" :scale="[20, 10, 2]" receive-shadow>
    <!-- @vue-ignore -->
    <TresMeshPhysicalMaterial color="rgba(170, 30, 44)" :roughness="1" />
  </Backdrop>
  <!-- @vue-ignore -->
  <TresDirectionalLight cast-shadow :position="[-0.5, 2, -1]" :intensity="5"
  :shadow-mapSize-width="2048" :shadow-mapSize-height="2048" :shadow-radius="4" />
</TresCanvas>
</template>
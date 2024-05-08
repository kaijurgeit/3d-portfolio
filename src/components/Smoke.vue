<script setup language="ts">
import * as THREE from 'three';
import { shallowRef } from 'vue';
import { useRenderLoop } from '@tresjs/core';

const smokeRef = shallowRef(null);
const scene = new THREE.Scene()

// Smoke
const smokeTexture = new THREE.TextureLoader().load("./public/Smoke/0000.png");
// @ts-ignore
smokeTexture.encoding = THREE.sRGBEncoding;
const smokeGeometry = new THREE.PlaneGeometry(300, 300);

const smokeMaterial = new THREE.MeshLambertMaterial({
    map: smokeTexture,
    emissive: 0x222222,
    opacity: 0.5,
    transparent: true
});

const randNum = () => { return Math.random() * 1000-500; }

let smokeParticles = [];
for (let i = 0; i < 90; i++) {
    let smokeElement = new THREE.Mesh(smokeGeometry, smokeMaterial);
    smokeElement.scale.set(2, 2, 2);
    smokeElement.position.set(randNum(),randNum(), Math.random() * 1000-500);
    smokeElement.rotation.z = Math.random() * 360;

    scene.add(smokeElement);
    smokeParticles.push(smokeElement);
}

// animate();
const { onLoop } = useRenderLoop();
onLoop(({ delta }) => {
    // @ts-ignore
  if(smokeRef && smokeRef.value && smokeRef.value.children ) {
    // @ts-ignore
    smokeRef.value.children.forEach(smokeElement => {
      smokeElement.rotation.z += (delta * 0.12)
    });
  }
})

</script>
<template>
<primitive ref="smokeRef" :object="scene" />
</template>
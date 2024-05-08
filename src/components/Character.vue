<script setup lang="ts">
import { ref } from 'vue';
import { useAnimations, useGLTF, useTweakPane } from '@tresjs/cientos';
// @ts-ignore
const { pane } = useTweakPane();

const { scene, animations } = await useGLTF ('./models/Manny.glb');
const { actions } = useAnimations(animations, scene);
const currentAction = ref(actions.MM_Idle_0);
currentAction.value.play();
scene.traverse( function( node: { isMesh: any; castShadow: boolean; } ) {

if ( node.isMesh ) { 
    node.castShadow = true; }

} );
</script>

<template>
<primitive :object="scene"/>
</template>
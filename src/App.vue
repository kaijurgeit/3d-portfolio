<script setup lang="ts">
import { ref } from 'vue';
import type { Ref } from 'vue';
import Canvas from "./components/Canvas.vue"

type Item = { 
  headline: string
  text: string
 }

const items: Ref<Item[]> = ref([]);
const navs = ref(['Contestants', 'Equipment']);

["apple", "orange", "cherry"].forEach(item => items.value.push({ 
  headline: item,
  text: 'Lorem, ipsum dolor'
}));
</script>

<template>
  <main>
    <div class="background">
      <Canvas />
    </div>
    <div class="content">
      <div class="items-container">
        <div v-for="item in items" class="item">
          <h3>{{ item.headline }}</h3>
          <p class="item-text">{{ item.text }}</p>
        </div>
      </div>
      <div class="nav">
        <h2 v-for="nav in navs" >{{ nav }}</h2>
      </div>
    </div>
  </main>
</template>

<style scoped>
p, h1, h2, h3 {  
  font-family: Saira;
  color: white;
}

h1, h2, h3 {  
  font-family: Saira;
  font-weight: bold;
  text-transform: uppercase;
}

p {  
  font-weight: 400;
}

h2 {
  font-size: 45px;
  font-style: italic;
  font-weight: 600;
  color: white;
  line-height: 50px;
  letter-spacing: -2px;
}

main {
  background-color: none;
  width: 100vw;
  height: 100vh;
}

.background {
  background-color: rgba(170, 30, 44, .1);
  width: 100vw;
  height: 100vh;
  position: absolute;
  z-index: -1;
}

.content {
  max-width: 1200px;
  padding: 50px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
}

.item {  
  background-color: rgba(0, 0, 0, 0.25);
  width: 360px;
  height: 120px;
  margin-bottom: 5px;
  border-radius: 5px;
  padding: 15px;
}

.nav {
  text-align: right;
}
</style>
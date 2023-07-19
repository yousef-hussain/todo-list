<script setup>
import {ref} from 'vue'
import Paragraph from './Paragraph.vue';
import CardTest from './CardTest.vue';
const comp = ref(Paragraph)
</script>
<template>
  <button @click="comp = Paragraph">paragraph</button>
  <button @click="comp = CardTest">card</button>
  <component :is="comp" />
  <component :is="comp"></component>
</template>

<style>
</style>
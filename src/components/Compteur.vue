<script setup>
import {ref} from 'vue'
const monCompteur = ref(0)
</script>

<template>
  <button @click="monCompteur++"> Vous m'avez cliqué {{monCompteur}} fois</button>
</template>

<style scoped>

</style>
<template>
  <div>
    {{ quiz }}
  </div>

</template>

<script setup>
import { onMounted, ref } from 'vue';

const quiz = ref(null)

onMounted(() => {
  fetch('/quiz.json')
  .then(r => {
    if(r.ok){
      return r.json()
    }
    throw new Error ('Impossible de charger le json')
  })
  .then(data => {
    quiz.value = data
  })
})

</script>
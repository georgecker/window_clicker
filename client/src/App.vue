<script setup>
import Win98Popup from './components/Win98Popup.vue'

function p() {
  console.log("Hehe");
}
</script>

<template>
  <main>
    <Win98Popup :x=200 :y=350 title="Paint" message="Save all my duck pics ?" btn-message="Yes" :timer-ms="2000"
      @timer-over="p" />
  </main>
</template>

<style scoped></style>

<!-- Dynamicly add and remove divs -->
<!-- https://stackoverflow.com/questions/61145426/adding-and-removing-divs-dynamically-in-vue-js-component -->

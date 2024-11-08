<script setup>
import { onBeforeMount, ref } from 'vue';
import Win98Popup from './components/Win98Popup.vue'

const windows = ref([]);

function removeWindow(id) {
  let result = windows.value.findIndex((w) => w.id == id);
  if (result >= 0) {
    windows.value.splice(result, 1);
    console.log(windows.value);
    return;
  }

  console.error(`Window with id ${id} not found`);
}

onBeforeMount(() => {
  windows.value.push({ id: 1, pos: { x: 100, y: 100 } }, { id: 2, pos: { x: 200, y: 200 } }, { id: 3, pos: { x: 300, y: 300 } });
});

</script>

<template>
  <main>
    <Win98Popup v-for="win in windows" :key="win" :id="win.id" :pos="win.pos" :timer-ms="3000" title="Paint"
      message="Save all my duck pics?" btn-message="Yes" v-on:closed="removeWindow" />
  </main>

  <audio controls>
    <!-- <source src="horse.mp3" type="audio/mpeg"> -->
    Your browser does not support the audio element.
  </audio>
</template>

<style scoped></style>

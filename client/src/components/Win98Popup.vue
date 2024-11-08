<script setup>
import { onMounted, ref } from 'vue';

const props = defineProps({
  id: { type: Number, required: true },
  pos: {
    x: { type: Number, required: true },
    y: { type: Number, required: true },
  },
  title: String,
  message: String,
  btnMessage: String,
  timerMs: Number,
});

let timer;
let mutPos = props.pos;
let mousePosBuffer = {
  x: 0,
  y: 0,
}

const win98popup = ref(null);
const headerBar = ref(null);

const emit = defineEmits({
  timerOver: [],
  closed: [],
});

onMounted(() => {
  console.log(headerBar.value);
  console.log(win98popup.value);
  if (props.timerMs != undefined) {
    timer = setTimeout(() => emit('timerOver'), props.timerMs);
  }
});

function onClose() {
  clearTimeout(timer);
  emit('closed', props.id);
}

function setElementDrag(event) {
  console.log("Set drag");
  event.preventDefault();
  mousePosBuffer.x = event.clientX;
  mousePosBuffer.y = event.clientY;
  document.onmousemove = elementDrag;
}

function removeElemntDrag() {
  console.log("Remove drag");
  document.onmousemove = null;
}

function elementDrag(event) {
  event.preventDefault();
  mutPos.x = mutPos.x - (mousePosBuffer.x - event.clientX);
  mutPos.y = mutPos.y - (mousePosBuffer.y - event.clientY);
  mousePosBuffer.x = event.clientX;
  mousePosBuffer.y = event.clientY;
}

</script>

<template>
  <div ref="win98popup" @mouseup="removeElemntDrag" class="win98popup shadow"
    :style="{ top: mutPos.y + 'px', left: mutPos.x + 'px' }">
    <div ref="headerBar" @mousedown="setElementDrag" class="bar">
      <p>{{ props.title }}</p>
    </div>
    <section>
      <p>{{ props.message }}</p>
    </section>
    <div class="buttons">
      <button class="shadow" @click="onClose">
        <p>{{ props.btnMessage }}</p>
      </button>
    </div>
  </div>
</template>

<style scoped>
.win98popup {
  position: absolute;
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-between;
  align-items: center;
  font-family: "Microsoft Sans Serif", sans-serif;
  background: #c2c6ca;
  font-size: 12px;
  -webkit-font-smoothing: none;
  width: 265px;
  height: 118px;
  box-shadow: 0.5px 0.5px 0 0.5px black, inset 1px 1px #C2C6CA, inset -1px -1px #85898d, inset 2px 2px white;

  button {
    background: #c2c6ca;
    border: none;
    padding: 0;
    border-radius: 0;
    outline: none;
  }

  .shadow {
    box-shadow: 0.5px 0.5px 0 0.5px black, inset 1px 1px white,
      inset -1px -1px #85898d;
  }

  .bar {
    display: flex;
    flex-flow: row nowrap;
    font-weight: bold;
    justify-content: space-between;
    width: calc(100% - 11px);
    height: 13px;
    color: white;
    background: #00a;
    padding: 2px 3px 3px;
    margin: 3px 2px 1px 3px;

    p {
      margin: 0;
    }

    button {
      width: 15px;
      height: 13px;

      &:active {
        box-shadow: 0.5px 0.5px 0 0.5px white, inset 1px 1px black,
          inset -1px -1px #c2c6ca, inset 2px 2px #85898d;

        svg {
          transform: translateX(1px) translateY(1px);
        }
      }

      svg {
        margin: 3px 3px 3px 4px;
      }
    }
  }

  .buttons {
    display: flex;
    flex-flow: row nowrap;
    margin: 1px 15px 14px 14px;

    button {
      width: 74px;
      height: 22px;
      display: grid;

      &:not(:last-child) {
        margin-right: 7px;
      }

      p {
        font-size: 12px;
        margin: auto;
      }

      img {
        margin: 4px 3px 3px 4px;
        display: none;
      }

      p,
      img {
        grid-column: 1;
        grid-row: 1;
      }

      &:focus {
        outline: none;
        box-shadow: 0.5px 0.5px 0 0.5px black, inset 1px 1px black, inset -1px -1px black, inset 2px 2px white, inset -2px -2px #85898d;

        img {
          display: block;
        }
      }

      &:active {
        box-shadow: 0.5px 0.5px 0 0.5px black, inset 1px 1px black,
          inset -1px -1px #85898d, inset 2px 2px #85898d;
        outline: none;

        p,
        img {
          transform: translateX(1px) translateY(1px);
        }
      }
    }
  }
}
</style>

<script setup>
import { onMounted, ref } from 'vue'

const state = ref('opening')
const currentText = ref('Aku pengen ngomong sesuatu nih...')
const iteration = ref(0)
const finishType = ref(false)
const audio = new Audio('/drunk-text.mp3')

onMounted(() => {
  // const tenorScript = document.createElement('script')
  // tenorScript.setAttribute('src', 'https://tenor.com/embed.js')
  // tenorScript.async = true
  //
  // document.head.appendChild(tenorScript)
  setTimeout(() => {
    typeWriter()
  }, 500)

})

function reset() {
  currentText.value = ''
  iteration.value = 0
  finishType.value = false
}

function typeWriter () {
  const speed = 50

  if (iteration.value < currentText.value.length) {
    document.querySelector('#writing').innerHTML += currentText.value.charAt(iteration.value)

    iteration.value++

    setTimeout(typeWriter, speed)
  } else {
    setTimeout(() => {
      finishType.value = true
    }, 150)
  }
}

function nextClick() {
    audio.play()

  reset()

  switch (state.value) {
    case 'opening':
      document.querySelector('#writing').innerHTML = ''
      state.value = 'please-read'
      currentText.value = 'Tapi baca sampai akhir yaa 🥺'

      typeWriter()
      break;
    case 'please-read':
      document.querySelector('#writing').innerHTML = ''
      state.value = 'love'
      currentText.value = 'Aku sayang sama kamu, pokoknya sayang bangeet 🫶'

      typeWriter()
      break;
    case 'love':
      document.querySelector('#writing').innerHTML = ''
      state.value = 'sorry'
      currentText.value = 'Aku minta maaf ya kalo sikap aku sering bikin kamu marah ataupun nyakitin kamu 💔'

      typeWriter()
      break;
    case 'sorry':
      document.querySelector('#writing').innerHTML = ''
      state.value = 'confess'
      currentText.value = 'Maaf selalu gabisa ngertiin kamu dan selalu maksain idealisku. Pasti bikin kamu cape kan? 😭'

      typeWriter()
      break;
    case 'confess':
      document.querySelector('#writing').innerHTML = ''
      state.value = 'hug'
      currentText.value = 'Aku tuluuuuss banget sayang sama kamu, entah gimana caranya aku pasti usahain hehe 😋'

      typeWriter()
      break;
    case 'hug':
      document.querySelector('#writing').innerHTML = ''
      state.value = 'last'
      currentText.value = 'Terakhir deh. Tegur aku kalo aku salah dan berlebihan 🥺. Ajari aku biar bisa temani prosesmu sampai akhir, berarti selama hidup ❤️. Makasih udah mau baca sampe akhir. Love and miss from Jogja ❤️'

      typeWriter()
      break;
    case 'last':
      finishType.value = true
      break;

    default:
      break;
  }
}
</script>

<template>
  <div class="container">
    <div class="textbox-container">
      <div class="header">
        <div class="tenor-gif-embed">
          <img v-if="state === 'opening'" src="/erm-fingers.gif" alt="begging" width="100%" height="100%">
          <img v-if="state === 'please-read'" src="/sweet-zahraa-cute-zahraa.gif" alt="begging" width="100%" height="100%">
          <img v-if="state === 'love'" src="/kiss.gif" alt="begging" width="100%" height="100%">
          <img v-if="state === 'sorry'" src="/i-miss-you.gif" alt="begging" width="100%" height="100%">
          <img v-if="state === 'confess'" src="/i-miss-you.gif" alt="begging" width="100%" height="100%">
          <img v-if="state === 'hug'" src="/peach-goma-peach-and-goma.gif" alt="begging" width="100%" height="100%">
          <img v-if="state === 'last'" src="/squeeze-hug.gif" alt="begging" width="100%" height="100%">
        </div>
        <!-- <div v-show="state === 'opening'" class="tenor-gif-embed" data-postid="16022705" data-share-method="host" data-width="100%"></div> -->
        <!-- <div v-show="state === 'please-read'" class="tenor-gif-embed" data-postid="13735643" data-share-method="host" data-width="100%"></div> -->
      </div>
      <div class="box">
        <h3 v-show="state === 'opening'" style="margin-bottom: 1rem; font-weight: bold;">
          Haloo Zizi &#9829;
        </h3>
        <div id="writing">

        </div>
        <div v-show="finishType || !state === 'last'" class="click" @click="nextClick">Klik buat lanjut</div>
        <span class="floating-love">
          &#9829;
        </span>
      </div>
    </div>
  </div>
</template>

<style>
.container {
  min-width: 100vw;
  min-height: 100vh;
  background-color: transparent;
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.textbox-container {
  width: 400;
  height: auto;
  margin: auto;
}

.header {
  text-align: center;
}

.click {
  margin-top: 1rem;
  cursor: pointer;
  font-size: 14px;
  text-align: right;
  transition: all 150ms ease-out;
}

.box {
  position: relative;
  text-align: center;
  margin-top: 3rem;
  padding: 1rem;
  width: 100%;
  height: 100%;
  background-color: #00000069;
  border: 2px solid #ffffff;
  border-radius: 8px;
  color: #ffffff;
}

.floating-love {
  font-size: 25px;
  position: absolute;
  top: -20px;
  right: -12px;
}

.tenor-gif-embed {
  width: 150px !important;
  height: 150px;
  border-radius: 99999px;
  overflow: hidden;
  margin-left: auto;
  margin-right: auto;
  box-shadow: 1px -1px 10px 1px rgba(0,0,0,0.53);
  -webkit-box-shadow: 1px -1px 10px 1px rgba(0,0,0,0.53);
  -moz-box-shadow: 1px -1px 10px 1px rgba(0,0,0,0.53);
  background-color: #ffffff;
  border: 2px solid #ffffff;
}

.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
</style>

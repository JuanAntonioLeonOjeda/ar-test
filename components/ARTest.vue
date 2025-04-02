<template>
  <client-only>
    <div id="ar-container">
      <div class="mindar-container">
        <div class="mindar-scene">
          <a-scene mindar-image="imageTargetSrc: /targets/targets.mind;" embedded color-space="sRGB"
            renderer="colorManagement: true, physicallyCorrectLights" vr-mode-ui="enabled: false"
            device-orientation-permission-ui="enabled: true">

            <a-assets>
              <img id="fondo" src="/images/reboot.png" />
              <img id="personaje" src="/images/diana.jpeg" />
              <audio id="narracion" src="/audio/train.mp3"></audio>
            </a-assets>

            <a-camera position="0 0 0" look-controls="enabled: false"></a-camera>

            <a-entity mindar-image-target="targetIndex: 0">
              <a-image src="#fondo" position="0 0 -0.1" width="1.5" opacity="0.5" rotation="0 0 0"></a-image>
              <a-image src="#personaje" position="0.2 0.3 0.05" width="0.7"></a-image>
              <a-plane position="0 -0.4 0.1" width="1.4" height="0.4" color="#ffffff" opacity="0.9">
                <a-text value="Año 1593\nAquí los isleños repelieron a Francis Drake..." color="#000000" align="center"
                  position="0 0 0.01" width="1.2" scale="2 2 1"></a-text>
              </a-plane>
            </a-entity>

            <a-entity>
              <a-plane color="yellow" position="0 -0.8 0.1" width="0.8" height="0.2"></a-plane>
              <a-text value="Escuchar historia 🔊" align="center" color="black" position="0 -0.8 0.15" width="2"
                scale="2 2 1"></a-text>
              <a-plane color="transparent" position="0 -0.8 0.16" width="0.8" height="0.2" @click="playAudio"></a-plane>
            </a-entity>

          </a-scene>
        </div>
      </div>
    </div>
  </client-only>
</template>

<script setup>
import { useHead } from '#app'

useHead({
  script: [
    {
      src: 'https://cdn.jsdelivr.net/npm/mind-ar-js@1.1.4/dist/mindar-image.prod.js',
      tagPosition: 'body-close'
    },
    {
      src: 'https://aframe.io/releases/1.2.0/aframe.min.js',
      tagPosition: 'body-close'
    }
  ],
  link: [
    {
      rel: 'stylesheet',
      href: 'https://cdn.jsdelivr.net/npm/mind-ar-js@1.1.4/dist/mindar-image.prod.css'
    }
  ]
})

const playAudio = () => {
  const audio = document.getElementById('narracion')
  if (audio) {
    audio.play().catch((e) => {
      console.warn('Error al reproducir el audio:', e)
    })
  }
}
</script>

<style scoped>
#ar-container {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  position: relative;
}

.mindar-container {
  width: 100%;
  height: 100%;
  position: relative;
}
</style>

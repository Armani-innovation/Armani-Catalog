<script setup>
import { onMounted, ref } from 'vue'
import { PageFlip } from 'page-flip'

const bookContainer = ref(null)

const pages = [
  `${import.meta.env.BASE_URL}images/001.jpg`,
  `${import.meta.env.BASE_URL}images/003.jpg`,
  `${import.meta.env.BASE_URL}images/004.jpg`,
  `${import.meta.env.BASE_URL}images/005.jpg`,
  `${import.meta.env.BASE_URL}images/006.jpg`,
  `${import.meta.env.BASE_URL}images/007.jpg`,
  `${import.meta.env.BASE_URL}images/008.jpg`,
  `${import.meta.env.BASE_URL}images/009.jpg`,
  `${import.meta.env.BASE_URL}images/010.jpg`,
  `${import.meta.env.BASE_URL}images/011.jpg`,
  `${import.meta.env.BASE_URL}images/012.jpg`,
  `${import.meta.env.BASE_URL}images/013.jpg`,
  `${import.meta.env.BASE_URL}images/014.jpg`,
  `${import.meta.env.BASE_URL}images/015.jpg`,
  `${import.meta.env.BASE_URL}images/016.jpg`,
  `${import.meta.env.BASE_URL}images/017.jpg`,
  `${import.meta.env.BASE_URL}images/018.jpg`,
  `${import.meta.env.BASE_URL}images/019.jpg`,
  `${import.meta.env.BASE_URL}images/020.jpg`,
  `${import.meta.env.BASE_URL}images/021.jpg`,
]

onMounted(() => {
  const sound = new Audio(`${import.meta.env.BASE_URL}sounds/flippingEffect.mp3`)
  sound.preload = 'auto'

  const flipBook = new PageFlip(bookContainer.value, {
    width: 494,
    height: 700,
    size: 'fixed',
    showCover: true,
    maxShadowOpacity: 0.5,
    useMouseEvents: true,
    flippingTime: 1000,
    startPage: 0,
    usePortrait: true,
    drawShadow: true,
    startZIndex: 0,
    rtl: false,
    mobileScrollSupport: false,
  })

  flipBook.loadFromImages([...pages].reverse())
  flipBook.flip(pages.length - (pages.length % 2 === 0 ? 1 : 2))

  flipBook.on('flip', () => {
    sound.currentTime = 0
    sound.play().catch((err) => {
      console.warn('sound play failed:', err)
    })
  })
})
</script>

<template>
  <div class="container">
    <div ref="bookContainer" class="flipBook-wrapper"></div>
  </div>
</template>

<style scoped>
.container {
  width: 95vw;
  height: 95vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.flipBook-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: max-content;
  height: max-content;
  max-width: 1000px;
}
</style>

<!--<script setup>-->
<!--import flipBook from 'flipbook-vue'-->
<!--const pages = [-->
<!--  `${import.meta.env.BASE_URL}images/001.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/003.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/004.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/005.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/006.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/007.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/008.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/009.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/010.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/011.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/012.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/013.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/014.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/015.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/016.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/017.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/018.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/019.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/020.jpg`,-->
<!--  `${import.meta.env.BASE_URL}images/021.jpg`,-->
<!--]-->
<!--</script>-->

<!--<template>-->
<!--  <flipBook class="flipbook" :pages="pages"></flipBook>-->
<!--</template>-->

<!--<style>-->
<!--.flipbook {-->
<!--  width: 90vw;-->
<!--  height: 90vh;-->
<!--}-->
<!--</style>-->

<script setup>
import { onMounted, ref } from 'vue'
import { PageFlip } from 'page-flip'

const bookContainer = ref(null)

const pages = [
  '/images/001.jpg',
  '/images/003.jpg',
  '/images/004.jpg',
  '/images/005.jpg',
  '/images/006.jpg',
  '/images/007.jpg',
  '/images/008.jpg',
  '/images/009.jpg',
  '/images/010.jpg',
  '/images/011.jpg',
  '/images/012.jpg',
  '/images/013.jpg',
  '/images/014.jpg',
  '/images/015.jpg',
  '/images/016.jpg',
  '/images/017.jpg',
  '/images/018.jpg',
  '/images/019.jpg',
  '/images/020.jpg',
  '/images/021.jpg',
]

onMounted(() => {
  const flipBook = new PageFlip(bookContainer.value, {
    width: 500,
    height: 600,
    size: 'fixed',
    showCover: true,
    maxShadowOpacity: 0.5,
    useMouseEvents: true,
    flippingTime: 1000,
    startPage: 0,
    usePortrait: true,
    drawShadow: true,
    startZIndex: 0,
    rtl: true,
    mobileScrollSupport: false,
  })

  flipBook.loadFromImages([...pages].reverse())
  flipBook.flip(pages.length - (pages.length % 2 === 0 ? 1 : 2))
})
</script>

<template>
  <div ref="bookContainer" class="flipBook-wrapper"></div>
</template>

<style scoped>
.flipBook-wrapper {
  margin: 10vh auto 0 auto;
  direction: rtl;
  width: 100%;
  max-width: 1000px;
}
</style>

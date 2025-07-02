<script setup>
import { onMounted, ref } from 'vue'
import { PageFlip } from 'page-flip'

const bookContainer = ref(null)

const pages = [
  `${import.meta.env.BASE_URL}images/001.jpg`,
  `${import.meta.env.BASE_URL}images/002.jpg`,
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

  // تابعی برای محاسبه سایز مناسب کتاب
  function getResponsiveSize() {
    const vw = window.innerWidth;
    const vh = window.innerHeight;
    const aspectRatio = 494 / 700;

    const isLandscape = vw > vh;

    let pageWidth
    let pageHeight

    if (isLandscape) {
      // حالت افقی: هر دو صفحه باید در عرض جا بشن، مثلاً 90٪ از عرض کل
      const maxTotalWidth = vw * 0.9;
      pageWidth = maxTotalWidth / 2;
      pageHeight = (pageWidth / aspectRatio) - 200 ;

      // در صورتی که ارتفاع بیشتر از صفحه بشه، با VH محدودش می‌کنیم
      if (pageHeight > vh * 0.9) {
        pageHeight = vh * 0.9;
        pageWidth = pageHeight * aspectRatio;
      }
    } else {
      // حالت عمودی: سایز تک صفحه مثل قبل
      pageWidth = vw * 0.25;
      pageHeight = pageWidth / aspectRatio;

      if (pageHeight > vh * 0.9) {
        pageHeight = vh * 0.9;
        pageWidth = pageHeight * aspectRatio;
      }
    }

    return {
      width: Math.floor(pageWidth),
      height: Math.floor(pageHeight),
    };
  }

  const { width, height } = getResponsiveSize();

  const flipBook = new PageFlip(bookContainer.value, {
    width,
    height,
    size: 'stretch', // مهم: stretch باعث رسپانسیو شدن میشه
    showCover: false,
    maxShadowOpacity: 0.5,
    useMouseEvents: true,
    flippingTime: 1000,
    startPage: 0,
    usePortrait: false, // مهم: false یعنی دو صفحه‌ای حتی در موبایل
    drawShadow: true,
    startZIndex: 0,
    rtl: false,
    mobileScrollSupport: true,
  });

  flipBook.loadFromImages([...pages].reverse());
  flipBook.flip(pages.length - (pages.length % 2 === 0 ? 2 : 1));

  flipBook.on('flip', () => {
    sound.currentTime = 0;
    sound.play().catch((err) => {
      console.warn('sound play failed:', err);
    });
  });

// 📱 هنگام تغییر سایز پنجره (مثلاً چرخاندن گوشی)، کتاب دوباره سایز بگیره
  window.addEventListener('resize', () => {
    const { width, height } = getResponsiveSize();
    flipBook.updateState({
      width,
      height,
    });
  });
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
  height: 98vh;
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
}
</style>

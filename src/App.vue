// SwiperComponent.vue
<template>
  <div class="swiper-container">
    <swiper-container
        :slides-per-view="1"
        :space-between="0"
        :scrollbar="false"
        :direction="'vertical'"
        :parallax="true"
        :speed="800"
        :effect="'slide'"
        @swiper="onSwiperInit"
        @slideChange="onSlideChange"
    >
      <swiper-slide>
        <FirstScreen></FirstScreen>
      </swiper-slide>
      <swiper-slide>
        <CalendarScreen></CalendarScreen>
      </swiper-slide>
      <swiper-slide v-for="(slide, index) in slides" :key="index">
        <div class="slide-content" :style="{ backgroundColor: slide.bgColor }">
          <div class="slide-text-content">
            <h3 :data-swiper-parallax="-300" :data-swiper-parallax-duration="600">{{ slide.title }}</h3>
            <p :data-swiper-parallax="-500" :data-swiper-parallax-duration="800">{{ slide.description }}</p>
          </div>
        </div>
      </swiper-slide>
    </swiper-container>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { register } from 'swiper/element/bundle';
import FirstScreen from "./components/FirstScreen.vue";
import CalendarScreen from "./components/CalendarScreen.vue";

// Регистрация Swiper Elements
register();

// Интерфейс для слайдов
interface Slide {
  id: number;
  title: string;
  description: string;
  bgColor: string;
}

// Реактивное состояние для слайдов
const slides = ref<Slide[]>([
  {
    id: 1,
    title: 'Слайд 1',
    description: 'Описание слайда 1 с параллакс-эффектом. Вертикальная прокрутка переключает слайды.',
    bgColor: '#4A6D7C'
  },
  {
    id: 2,
    title: 'Слайд 2',
    description: 'Описание слайда 2 с параллакс-эффектом. Каждый слайд занимает весь экран.',
    bgColor: '#663F46'
  },
  {
    id: 3,
    title: 'Слайд 3',
    description: 'Описание слайда 3 с параллакс-эффектом. Элементы появляются с разной скоростью.',
    bgColor: '#5B2E48'
  },
  {
    id: 4,
    title: 'Слайд 4',
    description: 'Описание слайда 4 с параллакс-эффектом. Текст имеет эффект параллакса.',
    bgColor: '#2E294E'
  },
  {
    id: 5,
    title: 'Слайд 5',
    description: 'Описание слайда 5 с параллакс-эффектом. Финальный слайд вертикальной галереи.',
    bgColor: '#1B2021'
  }
]);

// Храним экземпляр Swiper
let swiperInstance: any = null;

// Функция обработки инициализации Swiper
const onSwiperInit = (event: any) => {
  swiperInstance = event.detail[0];
  console.log('Swiper initialized', swiperInstance);
};

// Функция обработки изменения слайда
const onSlideChange = (event: any) => {
  const [swiper] = event.detail;
  console.log('Slide changed to:', swiper.activeIndex);
};

// Используем хук жизненного цикла
onMounted(() => {
  console.log('Swiper component mounted');

  // Для учета изменения размера окна
  window.addEventListener('resize', () => {
    if (swiperInstance) {
      swiperInstance.update();
    }
  });
});
</script>

<style scoped>
.swiper-container {
  width: 100%;
  height: 100vh; /* Высота на весь экран */
}

swiper-container {
  width: 100%;
  height: 100%;
}

swiper-slide {
  width: 100%;
  height: 100%;
}

.slide-content {
  width: 100%;
  height: 100%;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
}

.slide-text-content {
  z-index: 2;
  text-align: center;
  max-width: 800px;
  position: relative;
  will-change: transform;
}

h3 {
  font-size: 3rem;
  margin-bottom: 1rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  will-change: transform;
}

p {
  font-size: 1.5rem;
  line-height: 1.6;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  will-change: transform;
}

/* Стили для пагинации */
:global(.swiper-pagination-bullet) {
  width: 12px;
  height: 12px;
  background-color: white;
  opacity: 0.5;
}

:global(.swiper-pagination-bullet-active) {
  opacity: 1;
}

/* Стили для кнопок навигации */
:global(.swiper-button-next),
:global(.swiper-button-prev) {
  color: white;
}
</style>
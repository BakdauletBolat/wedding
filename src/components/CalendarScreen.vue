<template>
  <div class="w-full bg-white p-[24px] flex flex-col justify-between h-screen">
    <div class="calendar mt-[50px]">
      <div class="mb-6" data-swiper-parallax="-300">
        <h1 class="text-2xl font-bold text-[#B07F69]">Июнь 2025</h1>
      </div>

      <div class="grid grid-cols-7 gap-1 mb-2">
        <div
            v-for="(day, index) in weekdays"
            :key="day"
            class="text-center uppercase text-sm font-semibold"
            style="color: #797C3E"
            :data-swiper-parallax="calculateWeekdayParallax(index)"
            :data-swiper-parallax-opacity="0"
            :data-swiper-parallax-duration="calculateWeekdayDuration(index)"
        >
          {{ day }}
        </div>
      </div>

      <div class="grid grid-cols-7 gap-1">
        <div
            v-for="(day, index) in calendarDays"
            :key="index"
            class="relative aspect-square flex items-center justify-center rounded"
            :class="getDayClasses(day)"
            :data-swiper-parallax="calculateParallax(index)"
            :data-swiper-parallax-opacity="0"
            :data-swiper-parallax-duration="calculateDuration(index)"
        >
          <div v-if="day !== 0" class="relative z-10">
          <span v-if="day === 7" class="relative">
            <svg class="absolute -top-5 -left-5 h-15 w-15 text-red-300" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" style="z-index: -1">
              <path d="M11.8 21c-0.2-0.1-7.7-6-9.3-10.2-0.8-2.1-0.5-4.8 1.5-6.2 1.3-0.9 3.5-1 4.8 0.2 0.7 0.7 1.1 1.3 1.8 2.2 0.5-0.7 0.9-1.3 1.5-1.9 1.5-1.5 4-1.5 5.5-0.3 1.7 1.4 2.4 3.7 1.7 5.8-1.5 4.2-7.3 10.2-7.5 10.4z" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <span class="relative z-10 text-2xl caveat-regular">{{ day }}</span>
          </span>
            <span v-else class="text-xl">{{ day }}</span>
          </div>
        </div>
      </div>
    </div>
    <div :data-swiper-parallax="-800" class="flex justify-end relative">
      <div class="absolute top-0 left-[-150px]">
        <img class="w-[287px] z-[100px] object-contain" alt="bottom-image" :src="BottomImage"/>
      </div>
      <div class="max-w-[170px] mb-[100px] caveat-regular text-[22px] text-[#B07F69] pr-[18px] border-r border-r-[#797C3E]">
        Ожидаем всех в
        этот прекрасный
        день
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

import BottomImage from '../assets/screen-two/bottom.png';
const weekdays = ref(['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс']);
const calendarDays = ref(getJune2025Days());

function getJune2025Days() {
  // Создаем пустой массив для дней
  const days = Array(42).fill(0);

  // Определяем, с какого дня недели начинается июнь 2025
  const firstDayOfJune = new Date(2025, 5, 1);
  let startOffset = firstDayOfJune.getDay();

  // Корректируем, так как в JS воскресенье = 0, а в нашем календаре это 7-й день
  if (startOffset === 0) startOffset = 7;

  // Заполняем дни месяца (июнь 2025 имеет 30 дней)
  for (let i = 1; i <= 30; i++) {
    days[i + startOffset - 2] = i;
  }

  return days;
}

function getDayClasses(day: any) {
  if (day === 0) {
    return 'text-gray-300 hover:bg-gray-100';
  } else if (day === 7) {
    return 'text-gray-700 font-bold hover:bg-pink-100';
  } else {
    return 'bg-white text-gray-700 hover:bg-gray-100';
  }
}

function calculateParallax(index: number) {
  // Создаем эффект появления чисел по диагонали (базовые -700 с дополнительным смещением)
  const rowOffset = Math.floor(index / 7) * 50;
  const colOffset = (index % 7) * 50;
  return `-${500 + rowOffset + colOffset}`;
}

function calculateDuration(index: number) {
  // В два раза быстрее
  return 400 + (index * 15);
}

function calculateWeekdayParallax(index: number) {
  // Смещение для дней недели
  return `-${500 + (index * 100)}`;
}

function calculateWeekdayDuration(index: number) {
  // В два раза быстрее
  return 300 + (index * 15);
}
</script>
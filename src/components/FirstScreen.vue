<script setup lang="ts">
import TopImageElem1 from '../assets/flower-main-top/Group 8.png';
import BottomImage from '../assets/flower-main-bottom/bottom.png';
</script>

<template>
  <div class="slide-content relative">
    <div :data-swiper-parallax="-200" class="slide-top-image w-[400px] object-contain absolute z-[9999]
    flex items-center
    justify-center -top-[100px] -left-[70px]">
      <img alt="test absolute top-0 left-0" :src="TopImageElem1"/>
    </div>
    <div :data-swiper-parallax="-800" class="slide-top-image w-[330px] object-contain absolute z-[9999]
    flex items-center
    justify-center -bottom-[80px] -right-[70px]">
      <img alt="test absolute top-0 left-0" :src="BottomImage"/>
    </div>
    <div class="slide-text-content">
      <div class="text-black">
        <h3 class="poppins-regular text-sm" :data-swiper-parallax="-700">Дорогой Нурбахыт</h3>
        <div class="mt-2">
          <div class="lora-light text-[32px] text-[#797C3E] leading-none tracking-[5px]" :data-swiper-parallax="-600" >Приглашаем</div>
          <div class="flex items-center gap-[10px] leading-none mt-2" :data-swiper-parallax="-500" >
            <div class="text-[#B07F69] tracking-[4px] caveat-regular text-[20px]">на нашу</div>
            <div class="lora-light tracking-[5px] text-[32px] text-[#797C3E]">свадьбу</div>
          </div>
        </div>
        <div :data-swiper-parallax="-500"  class="text-sm poppins-regular mt-[28px] px-[15px] border-l-1 border-l-[#797C3E]">
          Ждем тебя 07.06.2025 в 18:00 <br/>
          по адресу: ул. Байгазиев 13А, <br/>
          Тойхана Аяулым, г. Арысь
        </div>
        <div :data-swiper-parallax="-400"  class="flex justify-end text-[#B07F69] mt-[20px] caveat-regular text-[20px]">
          Фаима и Бакдаулет
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
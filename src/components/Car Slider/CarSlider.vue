<template>
  <swiper
    :slides-per-view="1"
    :space-between="0"
    :loop="true"
    navigation
    class=" cars row-start-3 row-end-4 row-span-1 col-start-1 col-end-1 lg:row-end-3 lg:row-span-2 lg:col-start-2 lg:col-end-2 overflow-x-hidden w-full h-full "
  >
    <swiper-slide v-for="(car) in cars" :key="car.id">
      <div class="justify-center sm:justify-start first-part flex flex-wrap mt-2.5">
        <img v-for="item in 4" :key="item"
             :src="require('@/assets/img/cars/'+type+'/'+car.mark+'_'+car.model+'/'+item+'.png')"
             alt="Image of car"
             class="w-5/6 sm:w-1/2 h-72 lg:h-56 xl:h-60 2xl:h-64 mb-2 sm:mb-0">
      </div>
      <div class="second-part flex  flex-col items-center justify-center pb-10 pt-6 ">
        <h6 class="font-bold mb-2 text-white text-xl">{{car.mark}} {{car.model}}</h6>
        <p style="color: #e2e2e2">Цена под ключ с ремонтом: <span class="text-white">{{ car.priceWithRepair }}</span></p>
        <p style="color: #e2e2e2">Цена на внутреннем рынке: <span class="text-white">{{ car.priceOnDomesticMarket }}</span></p>
        <p style="color: #e2e2e2">Двигатель: <span class="text-white">{{ car.engine}}</span></p>
        <p style="color: #e2e2e2">Расход топлива: <span class="text-white">{{ car.fuelConsumption }}</span></p>
        <p class="text-white">{{car.additions}}</p>
      </div>
    </swiper-slide>
    <LabelStep :class="'bg-step2-loosing-opacity z-50'">Шаг 2</LabelStep>
  </swiper>

</template>

<script>
import LabelStep from '@/components/LabelStep'

import SwiperCore, { Navigation, A11y, Virtual } from 'swiper'

import { Swiper, SwiperSlide } from 'swiper/vue'

import 'swiper/swiper.scss'
import 'swiper/components/navigation/navigation.scss'

// install Swiper modules
SwiperCore.use([Navigation, A11y, Virtual])

export default {
  name: 'CarSlider',
  props: ['cars', 'type'],
  components: { Swiper, SwiperSlide, LabelStep },
  data () {
    return {
      transName: '',
      currentSlide: 0,
      currentType: this.type
    }
  },
  watch: {
    type: function () {
      if (this.type !== this.currentType) {
        this.currentSlide = 0
        this.currentType = this.type
      }
    }
  },
  methods: {
    changeSlide: function (direction) {
      if (direction === 'prev') {
        this.transName = 'car-slider-prev'
        if (this.currentSlide === 0) {
          this.currentSlide = this.cars.length - 1
        } else {
          this.currentSlide = this.currentSlide - 1
        }
      } else {
        this.transName = 'car-slider-next'
        if (this.currentSlide === this.cars.length - 1) {
          this.currentSlide = 0
        } else {
          this.currentSlide = this.currentSlide + 1
        }
      }
    }
  }
}

</script>

<style lang="scss" >
.cars .swiper-button-prev,.cars .swiper-button-next{
  &::after{
    content: '';
  }
  background: url("../../assets/img/controls/ControlArrow1.svg") no-repeat center;
  top: 85%;
}
.cars .swiper-button-prev{
  transform: rotate(180deg);
}
@media screen and (max-width: 767px){
  .cars .swiper-button-prev,.cars .swiper-button-next{
    top: 92%;
  }
}
</style>

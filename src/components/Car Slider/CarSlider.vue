<template>
  <div class="cars row-start-3 row-end-4 row-span-1 col-start-1 col-end-1 lg:row-end-3 lg:row-span-2 lg:col-start-2 lg:col-end-2 overflow-x-hidden w-full h-full relative">
        <transition :name="transName" v-for="(car,index) in cars" :key="car.id" >
        <div class="slide absolute z-30 w-full" v-if="currentSlide === index " >
          <div class="absolute z-40 top-0 left-0 right-0 bottom-0" @mousedown="swipeStart($event)" @mouseup="swipeEnd($event)" @touchstart="swipeStart($event)" @touchend="swipeEnd($event)">
          </div>
          <div class="justify-center sm:justify-start first-part flex flex-wrap mt-1">
            <img v-for="item in 4" :key="item"
                 :src="require('@/assets/img/cars/'+type+'/'+car.mark+'_'+car.model+'/'+item+'.png')"
                 alt="Image of car"
                 class="w-5/6 sm:w-1/2 h-72 lg:h-60 mb-2 sm:mb-0">
          </div>
          <div class="second-part flex  flex-col items-center justify-center pb-5 pt-5 ">
            <h6 class="font-bold mb-2 text-white text-xl">{{car.mark}} {{car.model}}</h6>
            <p style="color: #e2e2e2">Цена под ключ с ремонтом: <span class="text-white">{{ car.priceWithRepair }}</span></p>
            <p style="color: #e2e2e2">Цена на внутреннем рынке: <span class="text-white">{{ car.priceOnDomesticMarket }}</span></p>
            <p style="color: #e2e2e2">Двигатель: <span class="text-white">{{ car.engine}}</span></p>
            <p style="color: #e2e2e2">Расход топлива: <span class="text-white">{{ car.fuelConsumption }}</span></p>
            <p class="text-white">{{car.additions}}</p>
            <a href="#form">
              <div class="rounded-3xl bd-grad md:ml-4 text-white mt-4">
                <button class="rounded-3xl bg-grad px-14 py-2">Заказать</button>
              </div>
            </a>
          </div>
        </div>
        </transition>
      <div @click="changeSlide('next')" class="control absolute z-50 right-6 cursor-pointer">
        <img :src="require('@/assets/img/controls/ControlArrow1.svg')" class="w-4 lg:w-3" alt="">
      </div>
      <div @click="changeSlide('prev')" class="control absolute z-50 left-6 transform rotate-180 cursor-pointer">
        <img :src="require('@/assets/img/controls/ControlArrow1.svg')" class="w-4 lg:w-3" alt="">
      </div>
    <LabelStep :class="'bg-step2-loosing-opacity z-50'">Шаг 2</LabelStep>
  </div>
</template>

<script>
import LabelStep from '@/components/LabelStep'

export default {
  name: 'CarSlider',
  props: ['cars', 'type'],
  components: { LabelStep },
  data () {
    return {
      transName: '',
      currentSlide: 0,
      currentType: this.type,
      startPos: 0,
      endPos: 0
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
    swipeStart: function (e) {
      if (e.clientX) {
        this.startPos = e.clientX
      } else {
        this.startPos = e.touches[0].clientX
      }
    },
    swipeEnd: function (e) {
      if (e.clientX) {
        this.endPos = e.clientX
      } else {
        this.endPos = e.changedTouches[0].clientX
      }
      if (this.startPos > this.endPos) {
        this.changeSlide('next')
      } else if (this.startPos < this.endPos) {
        this.changeSlide('prev')
      }
    },
    changeSlide: function (direction) {
      if (direction === 'prev') {
        this.transName = 'slider-prev'
        if (this.currentSlide === 0) {
          this.currentSlide = this.cars.length - 1
        } else {
          this.currentSlide = this.currentSlide - 1
        }
      } else {
        this.transName = 'slider-next'
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

<style lang="scss" scoped>
.slider-next-enter-active,
.slider-next-leave-active,
.slider-prev-enter-active,
.slider-prev-leave-active {
  transition: all 0.5s ease;
  left: 0;
}
.slider-next-enter-from,
.slider-prev-leave-to{
  left: 100%;
}
.slider-next-leave-to,
.slider-prev-enter-from{
  left: -100%;
}
</style>

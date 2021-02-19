<template>
  <div class="wrapper flex relative overflow-x-hidden w-full h-full">
      <div v-for="(type,index) in carTypes"
           :key="type"
           class="h-full car-types">
        <transition :name="transName">
          <div v-if="index <= 4 "
               class="w-full sm:w-1/3 absolute z-10 slide h-full black-bg"
               :class="index === 0 ? 'sm:-left-1/3 slide1' : index === 1 ? 'sm:left-0 slide2' : index === 2 ? 'sm:left-1/3 slide3' : index === 3 ? 'sm:left-2/3 slide4' : index === 4 ? 'sm:left-full slide5' : ''">
            <div class="flex justify-center items-center relative w-full h-full flex-col px-4 py-4 sm:py-2 md:py-8"
                 :class="index === 3 ? '' : 'separator-types'"
                 @click="chose(type.label)"
                 @mousedown="swipeStart($event)" @mouseup="swipeEnd($event)" @touchstart="swipeStart($event)" @touchend="swipeEnd($event)">
              <svg class="cursor-pointer" :width="type.icon.width" :height="type.icon.height" :viewBox="type.icon.viewbox" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd"
                      clip-rule="evenodd"
                      :d="type.icon.path"
                      :fill=" chosed === type.label ? 'url(#paint0_linear)' : 'white'"
                      :fill-opacity="chosed === type.label ? '1' : '0.5'"/>
                <defs v-if="chosed === type.label">
                  <linearGradient id="paint0_linear" x1="0.0241695" y1="12.0105" x2="74.0109" y2="12.0105" gradientUnits="userSpaceOnUse">
                    <stop stop-color="#D6D4FF"/>
                    <stop offset="0.484375" stop-color="#EFC7ED"/>
                    <stop offset="1" stop-color="#FFD4D9"/>
                  </linearGradient>
                </defs>
              </svg>
              <h6 class="font-bold mt-2 mb-3 text-white text-opacity-50" :class="chosed === type.label ? 'text-opacity-100' : ''">{{type.name}}</h6>
              <p class="text-center text-xs text-white text-opacity-50 px-3 font-light">{{type.description}}</p>
            </div>
          </div>
        </transition>
      </div>
      <div class="controls ">
        <div class="left absolute top-1/2 left-3 md:left-4 lg:left-2 z-50 transform rotate-180 cursor-pointer -translate-y-1/2" @click="changeSlide('prev')">
          <img src="@/assets/img/controls/ControlArrow1.svg" class="w-4 lg:w-3" alt="">
        </div>
        <div class="right absolute top-1/2 right-3 md:right-4 lg:right-2 z-50 cursor-pointer transform -translate-y-1/2" @click="changeSlide('next')">
          <img src="@/assets/img/controls/ControlArrow1.svg" class="w-4 lg:w-3" alt="">
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'CarTypeSlider',
  props: ['types', 'chosed'],
  emits: ['chosedType'],
  data () {
    return {
      transName: '',
      carTypes: JSON.parse(JSON.stringify(this.types))
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
      if (this.startPos > this.endPos + 50) {
        this.changeSlide('next')
      } else if (this.startPos < this.endPos - 50) {
        this.changeSlide('prev')
      }
    },
    changeSlide: function (direction) {
      if (direction === 'prev') {
        this.transName = 'slide-prev'
        this.carTypes.unshift(this.carTypes.pop())
        setTimeout(function () {
          this.transName = ''
        }, 500)
      } else {
        this.transName = 'slide-next'
        this.carTypes.push(this.carTypes.shift())
        setTimeout(function () {
          this.transName = ''
        }, 500)
      }
    },
    chose: function (type) {
      this.$emit('chosedType', type)
    }
  }
}

</script>

<style lang="scss" scoped>
  .slide-prev-enter-active,
  .slide-prev-leave-active,
  .slide-next-enter-active,
  .slide-next-leave-active,
  .slide {
    transition: all 0.5s ease;
  }
  .slide-prev-enter-from,
  .slide-next-leave-to {
    left: -33.3%;
  }
  .slide-next-enter-from,
  .slide-prev-leave-to {
    left: 100%;
  }
  @media screen and (max-width: 639px) {
    .car-types{
      .slide1{
        left: -200%;
      }
      .slide2{
        left: -100%;
      }
      .slide3{
        left: 0%;
      }
      .slide4{
        left: 100%;
      }
      .slide5{
        left: 200%;
      }
    }
  }
</style>
<!--https://www.shutterstock.com/ru/image-vector/car-type-model-objects-icons-set-407978929-->

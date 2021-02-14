<template>
  <div class="wrapper flex relative overflow-x-hidden w-full h-full">
      <div v-for="(type,index) in carTypes"
           :key="type"
           class="h-full">
        <transition :name="transName">
          <div v-if="index <= 4 "
               class="w-1/3 absolute z-10 slide h-full black-bg"
               :class="index === 0 ? '-left-1/3' : index === 1 ? 'left-0' : index === 2 ? 'left-1/3' : index === 3 ? 'left-2/3' : index === 4 ? 'left-full' : ''">
            <div class="flex justify-center items-center relative w-full h-full flex-col   px-4 py-2 md:py-8"
                 :class="index === 3 ? '' : 'separator-types'"
                 @click="chose(type.label)">
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
              <p class="text-center text-xs text-white text-opacity-50 px-3" :class="chosed === type.label ? 'text-opacity-100' : ''">{{type.description}}</p>
            </div>
          </div>
        </transition>
      </div>
      <div class="controls ">
        <div class="left absolute top-1/2 left-2 z-50 transform rotate-180 cursor-pointer" @click="changeSlide('prev')">
          <img src="@/assets/img/controls/ControlArrow1.svg" alt="">
        </div>
        <div class="right absolute top-1/2 right-2 z-50 cursor-pointer" @click="changeSlide('next')">
          <img src="@/assets/img/controls/ControlArrow1.svg" alt="">
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
</style>
<!--https://www.shutterstock.com/ru/image-vector/car-type-model-objects-icons-set-407978929-->

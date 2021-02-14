<template>
  <div class="wrapper flex relative mt-3  mx-auto overflow-x-hidden w-full h-80">
      <div v-for="(slide,index) in slides"
           :key="slide">
        <transition :name="transName">
          <div v-if="index <= 4 "
               class="w-1/3 absolute z-10 slide  "
               :class="index === 0 ? '-left-1/3' : index === 1 ? 'left-0' : index === 2 ? 'left-1/3' : index === 3 ? 'left-2/3' : index === 4 ? 'left-full' : ''">

          </div>
        </transition>
      </div>
      <div class="controls ">
        <div class="left absolute top-1/2 left-0 z-50" @click="changeSlide('prev')"><p>prev</p></div>
        <div class="right absolute top-1/2 right-0 z-50" @click="changeSlide('next')"><p>next</p></div>
      </div>
  </div>
</template>

<script>

export default {
  name: 'Slider',
  props: ['way', 'format'],
  data () {
    return {
      transName: '',
      slides: [1, 2, 3, 4, 5]
    }
  },
  methods: {
    changeSlide: function (direction) {
      if (direction === 'prev') {
        this.transName = 'slide-prev'
        this.slides.unshift(this.slides.pop())
        setTimeout(function () {
          this.transName = ''
        }, 500)
      } else {
        this.transName = 'slide-next'
        this.slides.push(this.slides.shift())
        setTimeout(function () {
          this.transName = ''
        }, 500)
      }
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

<template>
  <div class="wrapper flex relative mt-3  mx-auto overflow-x-hidden"
       :style="'height:'+height+';' +
               'width:'+width">
      <div v-for="(slide,index) in slides"
           class="slide w-full absolute z-10 "
           :key="slide">
        <transition name="slider">
          <div v-if="currentSlide === index">
            <img  :src="require('@/assets/'+way+slide+format)"
                  class="w-full"
                  :style="'height:'+height"
                  alt="">
          </div>
        </transition>
      </div>
    <div class="pagination absolute z-20 bottom-1.5 flex justify-center w-full">
      <div v-for="(slide,index) in slides"
           :key="slide"
           class="circle rounded-3xl bg-gray-200 transition w-5 h-5 mx-1"
           :class="index === currentSlide ? 'bg-gray-400' : ''"
           @click="paginate(index)"></div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Slider',
  props: ['way', 'format', 'slides', 'height', 'width', 'interval', 'timeout'],
  data () {
    return {
      currentSlide: 0,
      sliding: true
    }
  },
  methods: {
    slideFunc: function () {
      setInterval(() => {
        if (this.currentSlide === this.slides - 1 && this.sliding === true) {
          this.currentSlide = 0
        } else if (this.sliding === true) {
          this.currentSlide++
        }
      }, this.interval)
    },
    paginate: function (index) {
      this.currentSlide = index
      this.sliding = false
      setTimeout(() => {
        this.sliding = true
      }, this.timeout)
    }
  },
  mounted () {
    this.slideFunc()
  }

}

</script>

<style lang="scss" scoped>
  .slider-enter-active, .slider-leave-active {
    transition: all .5s;
  }
  .slider-enter{
    transform: translateX(100%);
  }
  .slider-leave-to{
    transform: translateX(-100%);
  }
</style>

<template>
  <transition name="car-slider">
    <slot name="slide"></slot>
  </transition>
</template>

<script>

export default {
  name: 'C',
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
  .slide0{
    left: -33.3%;
  }
  .slide1{
    left: 0;
  }
  .slide2{
    left: 33.3%;
  }
  .slide3{
    left: 66.6%;
  }
  .slide4{
    left: 100%;
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

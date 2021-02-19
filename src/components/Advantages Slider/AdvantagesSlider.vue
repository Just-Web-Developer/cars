<template>
  <div class="component-wrapper flex py-12 bg-grad relative flex-col lg:flex-row"
       :id="advantages.folderName === 'advantages_1' ? 'advantages1' : 'advantages2'">
    <div class="header h-full mb-2 md:w-full lg:w-1/3 lg:pl-10 flex flex-col items-center lg:block">
      <h1 class="text-3xl font-bold mb-6 text-center md:text-left" style="color: rgba(40,40,40,1);">{{advantages.header}}</h1>
      <a href="#form">
        <button class="rounded-3xl border border-black px-8 py-2">{{ advantages.button }}</button>
      </a>
    </div>
    <div class="wrapper flex relative overflow-x-hidden w-full left-12"
      :class="advantages.folderName === 'advantages_1' ? 'advantages1' : 'advantages2'"
      @mouseover="sliding =false"
      @mouseout="sliding = true">
      <div class="absolute z-40 top-0 left-0 right-0 bottom-0" @mousedown="swipeStart($event)" @mouseup="swipeEnd($event)" @touchstart="swipeStart($event)" @touchend="swipeEnd($event)">
      </div>
      <div v-for="(advantage, index) in  advantages.cards"
           :key="advantage"
           class="h-full">
        <transition :name="transName">
          <div v-if="index <= 4 "
               class="absolute z-10 slide h-full"
               :class="index === 0 ? 'first' : index === 1 ? 'left-0' : index === 2 ? 'third' : index === 3 ? 'fourth' : index === 4 ? 'fifth' : ''">
            <div class="flex relative w-full flex-col text-white  p-8 dark-bg h-full rounded-2xl">
              <div class="flex items-center">
                <div class="img flex items-center justify-center w-14 h-14 p-1" style="background: rgba(94,94,94,1); border-radius: 50%">
                  <img :src="require('@/assets/img/' + advantages.folderName +'/'+ advantage.icon + '.svg')" class="" alt="">
                </div>
                <p v-if="advantages.folderName === 'advantages_2'" class="text-white font-light text-sm ml-2.5">{{advantage.timeRange}}</p>
              </div>
              <h2 class="my-5 text-xl uppercase font-bold">{{advantage.header}}</h2>
              <p class="text-sm">{{advantage.description}}</p>
            </div>
          </div>
        </transition>
      </div>
      <div class="bg absolute left-1/3 top-0 bottom-0  bg-getting-opacity z-30 right-5 sm:right-12"></div>
    </div>
    <div class="controls ">
      <div class="arrow left absolute lg:top-1/2 left-3 lg:left-1/4 z-40 cursor-pointer transform -translate-y-1/2"
           @click="changeSlide('prev', true)">
        <img src="@/assets/img/controls/arrow2.svg" alt="">
      </div>
      <div class="arrow right absolute lg:top-1/2 right-3 lg:right-10 z-40 cursor-pointer transform rotate-180 transform -translate-y-1/2"
           @click="changeSlide('next', true)">
        <img src="@/assets/img/controls/arrow2.svg" alt="">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'AdvantagesSlider',
  props: ['advantages'],
  data () {
    return {
      advantagesData: this.advantages,
      transName: '',
      sliding: true
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
        this.changeSlide('next', true)
      } else if (this.startPos < this.endPos - 50) {
        this.changeSlide('prev', true)
      } else {
        this.stopSlider()
      }
    },
    changeSlide: function (direction, stop) {
      if (direction === 'prev') {
        this.transName = 'slide-prev'
        this.advantagesData.cards.unshift(this.advantagesData.cards.pop())
        setTimeout(function () {
          this.transName = ''
        }, 500)
      } else {
        this.transName = 'slide-next'
        this.advantagesData.cards.push(this.advantagesData.cards.shift())
        setTimeout(function () {
          this.transName = ''
        }, 500)
      }
      if (stop) {
        this.stopSlider()
      }
    },
    autoSlider: function () {
      setInterval(() => {
        if (this.sliding === true) {
          this.changeSlide('next', false)
        }
      }, 2000)
    },
    stopSlider: function () {
      this.sliding = false
      setTimeout(() => {
        this.sliding = true
      }, 3000)
    }
  },
  mounted () {
    this.autoSlider()
  }
}
</script>

<style lang="scss">
  .component-wrapper{
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
  }
  .advantages1{
    .slide{
      width: 33.33%;
    }
    .first{
      left: -37%;
    }
    .third{
      left: 37%;
    }
    .fourth{
      left: 74%;
    }
    .fifth{
      left: 111%;
    }
  }
  .advantages2{
    .slide{
      width: 30.33%;
    }
    .first{
      left: -34%;
    }
    .third{
      left: 34%;
    }
    .fourth{
      left: 68%;
    }
    .fifth{
      left: 102%;
    }
  }
@media screen and (max-width: 767px){
  .advantages1{
    .slide{
      width: 70%;
    }
    .first{
      left: -80%;
    }
    .third{
      left: 80%;
    }
    .fourth{
      left: 160%;
    }
    .fifth{
      left: 240%;
    }
  }
  .advantages2{
    .slide{
      width: 70%;
    }
    .first{
      left: -80%;
    }
    .third{
      left: 80%;
    }
    .fourth{
      left: 160%;
    }
    .fifth{
      left: 240%;
    }
  }
}
</style>

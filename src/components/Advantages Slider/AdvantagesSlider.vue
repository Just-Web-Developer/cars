<template>
  <div class="component-wrapper flex py-12 bg-grad relative flex-col lg:flex-row"
       :id="advantages.folderName === 'advantages_1' ? 'advantages1' : 'advantages2'">
    <div class="header h-full mb-2 md:w-full lg:w-1/3 lg:pl-10 flex flex-col items-center lg:block">
      <h1 class="text-3xl font-bold mb-6 text-center md:text-left" style="color: rgba(40,40,40,1);">{{advantages.header}}</h1>
      <a href="#form">
        <button class="rounded-3xl border border-black px-5 py-1">{{ advantages.button }}</button>
      </a>
    </div>
    <div class="wrapper flex relative overflow-x-hidden w-full left-12 md:mt-4"
      :class="advantages.folderName === 'advantages_1' ? 'advantages1' : 'advantages2'">
      <div v-for="(advantage, index) in  advantages.cards"
           :key="advantage"
           class="h-full">
        <transition :name="transName">
          <div v-if="index <= 4 "
               class="absolute z-10 slide h-full"
               :class="index === 0 ? 'first' : index === 1 ? 'left-0' : index === 2 ? 'third' : index === 3 ? 'fourth' : index === 4 ? 'fifth' : ''">
            <div class="flex relative w-full flex-col text-white  px-4 py-8 dark-bg h-full rounded-2xl">
              <div class="flex items-center">
                <img :src="require('@/assets/img/' + advantages.folderName +'/'+ advantage.icon + '.png')" alt="">
              </div>
              <h2 class="my-6 text-xl uppercase">{{advantage.header}}</h2>
              <p>{{advantage.description}}</p>
            </div>
          </div>
        </transition>
      </div>
      <div class="bg absolute left-1/3 top-0 bottom-0  bg-getting-opacity z-30 right-5 sm:right-12"></div>
    </div>
    <div class="controls ">
      <div class="arrow left absolute lg:top-1/2 left-3 lg:left-1/4 z-40 cursor-pointer transform -translate-y-1/2" @click="changeSlide('prev')">
        <img src="@/assets/img/controls/arrow2.svg" alt="">
      </div>
      <div class="arrow right absolute lg:top-1/2 right-3 lg:right-10 z-40 cursor-pointer transform rotate-180 transform -translate-y-1/2" @click="changeSlide('next')">
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
      transName: ''
    }
  },
  methods: {
    changeSlide: function (direction) {
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
    }
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

    .slide{
      img{
        width: 3.5rem;
      }
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
      width: 60%;
    }
    .first{
      left: -70%;
    }
    .third{
      left: 70%;
    }
    .fourth{
      left: 150%;
    }
    .fifth{
      left: 230%;
    }
  }
  .advantages2{
    .slide{
      width: 60%;
    }
    .first{
      left: -70%;
    }
    .third{
      left: 70%;
    }
    .fourth{
      left: 150%;
    }
    .fifth{
      left: 230%;
    }
  }
}
</style>
:class="index === 0 ? 'left:-37%;' : index === 1 ? 'left:0;' : index === 2 ? 'left:37%;' : index === 3 ? 'left:74%;' : index === 4 ? 'left:111%;' : ''">

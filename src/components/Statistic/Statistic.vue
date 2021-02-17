<template>
  <div class="flex w-full statistic flex-wrap md:flex-nowrap">
    <div v-for="(stat,index) in stats"
         class="stat relative w-1/2 md:w-1/4 black-bg py-10 text-white flex items-center flex-col"
         :key="stat.id"
         :class="index !== 3 > 768 ? 'separator' : ''">
      <h2 class="text-grad text-6xl bg-grad font-extrabold">{{stat.value}}</h2>
      <p class="uppercase font-bold">{{stat.name}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Statistic',
  props: ['stats']
}
</script>

<style lang="scss" scoped>
.statistic{
  h2{
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
}
</style>

<template>
  <div id="form" class="bg-grad w-full py-10">
    <div class="form-content dark-bg flex mx-auto w-5/6 md:w-3/5 items-center flex-col py-7 rounded-xl">
      <h1 class="font-bold text-3xl text-white">Оставить заявку</h1>
      <form action="" @submit.prevent="" class="w-5/6 flex flex-col mt-7 items-center">
        <div class="input flex flex-col mb-6">
          <label for="name" class="text-white ml-5">Имя и фамилия</label>
          <input type="text" id="name" class="px-2 py-3 w-64 sm:w-80 lg:w-96 mt-2 rounded-xl appearance-none cursor-pointer">
        </div>
        <div class="input flex flex-col mb-6">
          <label for="tel" class="text-white ml-5">Телефон</label>
          <input type="tel" id="tel" class="px-2 py-3 w-64 sm:w-80 lg:w-96 mt-2 rounded-xl appearance-none cursor-pointer">
        </div>
        <div class="input flex flex-col mb-6">
          <label for="email" class="text-white ml-5">E-mail</label>
          <input type="email" id="email" class="px-2 py-3 w-64 sm:w-72 sm:w-80 lg:w-96 mt-2 rounded-xl appearance-none cursor-pointer">
        </div>
        <div class="input flex flex-col mb-6">
          <label for="wishes" class="text-white ml-5">E-mail</label>
          <textarea name="" id="wishes" cols="30" rows="3" class="px-2 py-3 w-64 sm:w-80 mt-2 lg:w-96 rounded-xl appearance-none cursor-pointer"></textarea>
        </div>
        <button type="submit" class="rounded-3xl bg-grad px-12 py-2 dark-text mb-10">Отправить</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Form'
}
</script>

<style lang="scss" scoped>

</style>

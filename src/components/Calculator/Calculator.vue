<template>
  <div class="flex w-full black-bg justify-center items-center py-10 px-10 lg:px-32 flex-col" id="calculator">
    <h1 class="font-bold text-3xl text-white">Калькулятор доставки и растаможки авто</h1>
      <form action="" @submit.prevent="" class="flex justify-center flex-col items-center w-full xl:w-4/5 2xl:w-3/5">
        <div class="inputs w-full flex flex-col my-10">
          <div class="row w-full flex flex-col items-center md:flex-row md:items-baseline md:justify-around mb-6">
            <div class="input flex flex-col mb-6 md:mb-0">
              <label for="price" class="text-white ml-5 text-sm">Стоимость авто с аукциона ($)</label>
              <input type="text" id="price" class="px-2 py-3 w-80 mt-2 rounded-xl appearance-none cursor-pointer">
            </div>
            <div class="input">
              <label for="year" class="text-white ml-5 text-sm">Модельный год</label>
              <div class="select-wrapper relative mt-2">
                <select name="some" id="year" class="px-2 py-3 w-80 rounded-xl appearance-none cursor-pointer">
                  <option value="" disabled selected hidden>Выбрать</option>
                  <option value="some option 1">Some option 1</option>
                  <option value="some option 2">Some option 2</option>
                  <option value="some option 3">Some option 3</option>
                </select>
              </div>
            </div>
          </div>
          <div class="row w-full flex flex-col justify-around items-center md:flex-row md:items-baseline md:justify-around mb-6">
            <div class="input mb-6 md:mb-0">
              <label for="fuel-type" class="text-white ml-5 text-sm">Тип топлива</label>
              <div class="select-wrapper relative mt-2">
                <select name="some" id="fuel-type" class="px-2 py-3 w-80 rounded-xl appearance-none cursor-pointer">
                  <option value="" disabled selected hidden>Выбрать</option>
                  <option value="some option 1">Some option 1</option>
                  <option value="some option 2">Some option 2</option>
                  <option value="some option 3">Some option 3</option>
                </select>
              </div>
            </div>
            <div class="input">
              <label for="engine volume" class="text-white ml-5 text-sm">Объем двигателя (см3)</label>
              <div class="select-wrapper relative mt-2">
                <select name="some" id="engine volume" class="px-2 py-3 w-80 rounded-xl appearance-none cursor-pointer">
                  <option value="" disabled selected hidden>Выбрать</option>
                  <option value="some option 1">Some option 1</option>
                  <option value="some option 2">Some option 2</option>
                  <option value="some option 3">Some option 3</option>
                </select>
              </div>
            </div>
          </div>
          <div class="row w-full flex flex-col justify-around items-center md:flex-row md:items-baseline md:justify-around">
            <div class="input mb-6 md:mb-0">
              <label for="auction" class="text-white ml-5 text-sm">Аукцион</label>
              <div class="select-wrapper relative mb-2">
                <select name="some" id="auction" class="px-2 py-3 w-80 rounded-xl appearance-none cursor-pointer">
                  <option value="" disabled selected hidden>Выбрать</option>
                  <option value="some option 1">Some option 1</option>
                  <option value="some option 2">Some option 2</option>
                  <option value="some option 3">Some option 3</option>
                </select>
              </div>
            </div>
            <div class="input">
              <label for="location" class="text-white ml-5 text-sm">Местонахождение</label>
              <div class="select-wrapper relative mb-2">
                <select name="some" id="location" class="px-2 py-3 w-80 rounded-xl appearance-none cursor-pointer">
                  <option value="" disabled selected hidden>Выбрать</option>
                  <option value="some option 1">Some option 1</option>
                  <option value="some option 2">Some option 2</option>
                  <option value="some option 3">Some option 3</option>
                </select>
              </div>
            </div>
          </div>
        </div>
        <button type="submit" class="rounded-3xl bg-grad px-12 py-2 dark-text mb-10">Расчитать</button>
      </form>

    <span class="text-white text-sm mb-2">Приблизительная расчетная стоимость</span>
    <div class="output px-20 md:px-36 py-3 flex justify-center items-center rounded-xl">
      <p class="output-text bg-grad font-extrabold">{{ result.toLocaleString() }} $</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      result: 0
    }
  }
}
</script>

<style lang="scss" scoped>
  .select-wrapper{
    select{
      &::-ms-expand {
        display: none;
      }
    }
    &:after{
      content: '>';
      transform: rotate(90deg) translateX(-50%);
      display: flex;
      justify-content: center;
      align-items: center;
      position: absolute;
      right: 1rem;
      top: 50%;
      font-size: 1.5rem;
      width: 1rem;
      height: 1rem;
      pointer-events: none;
    }
  }
  .output-text{
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
</style>

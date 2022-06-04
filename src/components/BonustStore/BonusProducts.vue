<template>
  <div class="">
    <div class="mx-2 mt-6 text-center">
      <b>Всего бонусов:</b>
      <br/>
      {{ bonusValue }}
    </div>
    <input type="number" v-model="bonusInputValue"/>
    <button class="text-center px-4 py-2 rounded-md transition-all shadow-md ring-2
    font-semibold text-white bg-orange-500 ring-orange-500 active:bg-orange-400 active:ring-orange-400"
            @click="setBonusValue"

    >
      Добавить
    </button>
  </div>
</template>

<script>
export default {
  name: "BonusProducts",
  data() {
    return {
      bonusValue: 0,
      bonusInputValue: 0,
    };
  },
  methods: {
    setBonusValue() {
      this.bonusValue = Number.isInteger(+this.bonusInputValue)?this.bonusInputValue:this.bonusValue
    }
  }
}
</script>

<style scoped>

</style>
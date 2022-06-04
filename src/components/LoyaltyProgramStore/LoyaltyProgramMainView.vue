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
    <div class="qr text-center flex flex-col items-center">
      <button class="text-center px-4 py-2 rounded-md transition-all shadow-md ring-2
    font-semibold text-white bg-orange-500 ring-orange-500 active:bg-orange-400 active:ring-orange-400"
              @click="generateQr"
      >
        <template v-if="showQr">
          Скрыть QR
        </template>
        <template v-else>
          Показать QR
        </template>
      </button>
      <template v-if="showQr">
        <p>QR</p>
        <QrcodeVue :value="qrValue" :size="qrSize"/>
      </template>
    </div>
  </div>
</template>

<script>
import QrcodeVue from 'qrcode.vue'

export default {
  name: "LoyaltyProgramMainView",
  components: {
    QrcodeVue
  },
  data() {
    return {
      bonusValue: 0,
      bonusInputValue: 0,
      showQr: false,
      productId: 10,
      qrValue: 0,
      qrSize: 300,
    };
  },
  props: {
    userId: {
      type: Number
    },
  },
  methods: {
    setBonusValue() {
      this.bonusValue = Number.isInteger(+this.bonusInputValue) ? this.bonusInputValue : this.bonusValue
    },
    generateQr() {
      this.qrValue = `${this.userId} ${this.productId}`
      this.showQr = !this.showQr
    }
  }
}
</script>

<style scoped>

</style>
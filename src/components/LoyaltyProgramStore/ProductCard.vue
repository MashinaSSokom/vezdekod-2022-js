<template>
  <div
    class="w-fit ring-2 shadow-md ring-yellow-600 rounded-md flex flex-row h-28 m-2"
  >
    <div class="w-4/12">
      <img
        class="object-cover h-full rounded-l-md"
        height="100"
        src="../../assets/prodlogo.jpg"
        alt="survey"
      />
    </div>
    <div class="w-6/12 ">
      <div class="line-clamp-1 font-semibold">{{ productName }}</div>
      <div class="line-clamp-4 text-sm">{{ productDesc }}</div>
      <div class="line-clamp-4 text-sm">{{ productPrice }}</div>
      <button class="w-24 h-10  rounded-md transition-all
                     font-semibold text-white bg-orange-500 ring-orange-500 active:bg-orange-400 active:ring-orange-400"
              v-b-modal="`qr-${this.userId}-${this.productId}`"
              @click="generateQr"
      >

        <b-modal :id="`qr-${this.userId}-${this.productId}`" title="BootstrapVue" class="text-center" hide-footer>
          <QrcodeVue :value="qrValue" :size="150" class="flex justify-center"/>
        </b-modal>
          Купить
      </button>
<!--      <template v-if="showQr">-->
<!--        <QrcodeVue :value="qrValue" :size="300"/>-->
<!--      </template>-->
    </div>
  </div>
</template>

<script>
import QrcodeVue from "qrcode.vue";

export default {
  name: "ProductCard",
  components: {
    QrcodeVue
  },
  data() {
    return {
      qrValue: null,
      showQr: false
    }
  },
  props: {
    userId: {
      type: Number
    },
    productId: {
      type: Number
    },
    productName: {
      type: String
    },
    productDesc: {
      type: String
    },
    productPrice: {
      type: Number
    }
  },
  methods: {
    generateQr() {
      this.qrValue = JSON.stringify({userid: this.userId, productId: this.productId})
      this.showQr = !this.showQr
    }
  }
}
</script>

<style scoped>

</style>
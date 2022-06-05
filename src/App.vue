<template>
  <div id="app">
    <Header>s
      <CloseButton/>
    </Header>
    <Content :header="true" :footer="false" :scroll="true" :scrollbar="true">
      <div class="choose-role flex-column text-center">
        <p>Выберите роль</p>
        <button class="w-24 h-10 m-2 text-center rounded-md transition-all
                     font-semibold text-white bg-orange-500 ring-orange-500 active:bg-orange-400 active:ring-orange-400"
                @click="chooseCashier"
        >
          Кассир
        </button>
        <button class="w-24 h-10 m-2 text-center rounded-md transition-all
                     font-semibold text-white bg-orange-500 ring-orange-500 active:bg-orange-400 active:ring-orange-400"
                @click="chooseBuyer"
        >
          Покупатель
        </button>
      </div>
      <template v-if="this.role==='Кассир'">
        <div class="text-center mt-4 text-xl font-bold">Vue miniapp template</div>
        <div class="mt-6 text-center">
          <Button class="w-28" @setBarcode="setBarcode">
            <template slot="text">Read QR</template>
            <!--<template slot="icon">icon html</template>-->
          </Button>
        </div>
        <div v-if="barcode" class="mx-2 mt-6 text-center">
          <b>Result:</b>
          <br/>
          {{ this.barcode.result }}
        </div>
      </template>
      <template v-else-if="role==='Покупатель'">
        <div class="text-center">
          <LoyaltyProgramMainView :userId="this.userId"/>
        </div>
        <div class="flex-row">
          <ProductsList :user-id="this.userId"></ProductsList>
        </div>
      </template>


    </Content>
    <!--<Footer>content footer</Footer>-->
    <!--<Modal :isVisible="modal.show" @onClose="modal.show = false" />-->
    <!--<Spinner v-if="spinner" />-->
  </div>
</template>

<script lang="ts">
import Header from "./components/Header";
import CloseButton from "./components/CloseButton";
import Content from "./components/Content";
import Button from "./components/Button";
import LoyaltyProgramMainView from "./components/LoyaltyProgramStore/LoyaltyProgramMainView.vue";
import ProductsList from "./components/LoyaltyProgramStore/ProductsList.vue";
// import SurveyCard from "./components/SurveyCard";
// import Shimmer from "./components/Shimmer";
// import Spinner from "./components/Spinner";
// import Modal from "./components/Modal";
// import Footer from "./components/Footer";
import moby from "@mobyapps/moby.js";

export default {
  name: "App",
  components: {
    ProductsList,
    LoyaltyProgramMainView,
    // SurveyCard,
    // Shimmer,
    // Spinner,
    // Modal,
    // Footer,
    Content,
    Header,
    CloseButton,
    Button,
  },
  async beforeMount() {
    const fetchapp = await moby.info.app()
    this.app = fetchapp
    const miniapp = await moby.info.miniapp()
    this.miniapp = miniapp

    const storageType = moby.storage.setType(moby.sqlite.db_type.provider);
    await moby.storage.create();
    this.storageType = storageType

    this.storageType = storageType
    // await moby.storage.create(); // create SQLite table for 'provider' access level
    this.userId = Date.now()
    const status = await moby.storage.set("userId", `${this.userId}`);
    this.status = status
    let items = await moby.storage.items();

    console.log(items)

    this.storageItems = items

  },
  data() {
    return {
      barcode: "",
      // modal: {
      //   show: false,
      // },
      userId: null,
      spinner: true,
      role: null,
      app: {},
      miniapp: {},
      storageType: '',
      storageItems: {},
      status: ''
    };
  },
  methods: {
    setBarcode(barcode) {
      this.barcode = barcode;
    },
    chooseCashier() {
      this.role = 'Кассир'
    },
    chooseBuyer() {
      this.role = 'Покупатель'
    }
  },
};
</script>

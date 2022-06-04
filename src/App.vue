<template>
  <div id="app">
    <Header>
      <CloseButton/>
    </Header>
    <Content :header="true" :footer="false" :scroll="true" :scrollbar="true">
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
      <div class="text-center">
        <LoyaltyProgramMainView :userId="this.userId"/>
      </div>

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
// import SurveyCard from "./components/SurveyCard";
// import Shimmer from "./components/Shimmer";
// import Spinner from "./components/Spinner";
// import Modal from "./components/Modal";
// import Footer from "./components/Footer";
export default {
  name: "App",
  components: {
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
  beforeMount() {
    this.userId = Date.now()
  },
  data() {
    return {
      barcode: "",
      // modal: {
      //   show: false,
      // },
      userId: null,
      spinner: true,
    };
  },
  methods: {
    setBarcode(barcode) {
      this.barcode = barcode;
    },
  },
};
</script>

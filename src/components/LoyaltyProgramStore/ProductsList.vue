<template>
  <div class="product-list">
    <template v-for="product in this.products">
      <ProductCard :product-name="product.name"
                   :product-desc="product.description"
                   :product-price="product.price"
                   :key="product.id"
      />
    </template>
  </div>
</template>

<script>
import ProductCard from "@/components/LoyaltyProgramStore/ProductCard";
export default {
  name: "ProductsList",
  components: {ProductCard},
  data() {
    return {
      products: [
        {id: 1, name: 'Product 1', description: 'Product 1 desc', price: 100},
        {id: 2, name: 'Product 2', description: 'Product 1 desc', price: 200},
        {id: 3, name: 'Product 3', description: 'Product 1 desc', price: 300}
      ]
    }
  }
}
</script>

<style scoped>

</style>
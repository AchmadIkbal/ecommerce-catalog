<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
    </div>

    <div class="">
      <div class="mt-3" v-if="product">
        <!-- Pemilihan komponen berdasarkan kategori -->
        <component :is="currentProductComponent" :product="product" @next-product="loadNextProduct" />
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import axios from "axios";
import MenProductVue from "@/components/MenProduct.vue";
import WomenProductVue from "@/components/WomenProduct.vue";
import OtherProduct from "@/components/OtherProduct.vue";
export default {
  name: "HomeView",
  components: {
    Navbar,
    Hero,
    MenProductVue,
    WomenProductVue,
    OtherProduct
  },
  data() {
    return {
      productId: 5,
      product: null,
    };
  },
  computed: {
    currentProductComponent() {
      // Menentukan komponen yang akan di-render berdasarkan kategori produk
      if (this.product && this.product.category === "men's clothing") {
        return MenProductVue;
      } else if (this.product && this.product.category === "women's clothing") {
        return WomenProductVue;
      } else{
        return OtherProduct;
      }
      // Anda dapat menambahkan logika untuk kategori lainnya jika diperlukan
      // return null;
    },
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    loadNextProduct() {
      this.productId++;
      axios
        .get(`https://fakestoreapi.com/products/${this.productId}`)
        .then((response) => this.setProduct(response.data))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get(`https://fakestoreapi.com/products/${this.productId}`)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

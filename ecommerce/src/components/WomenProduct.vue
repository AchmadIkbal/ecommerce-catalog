<template>
  <div class="product">
    <div v-if="loading" class="loader"></div>
    <div v-else class="card">
      <div class="row">
        <div class="col-md-5">
          <div class="image-container">
            <img :src="product.image" alt="" />
          </div>
        </div>
        <div class="col-md-7">
          <div class="text-container">
            <div>
              <h4 class="pink">{{ product.title }}</h4>
              <div class="category">
                <p class="categoryContent col-md-6">{{ product.category }}</p>
                <div class="col-md-6 rating">
                  <!-- <span class="rating-circle">Rating: {{ product.rating.rate }}</span> -->
                </div>
              </div>
              <hr />
              <p class="description">{{ product.description }}</p>
              <p class="pink">${{ product.price }}</p>
              
              <button class="buy">Buy Now</button>
              <button class="next" @click="nextProduct">
                <span v-if="loading" class="loader"></span> <!-- Loader untuk tombol Next Product -->
                <span v-else>Next Product</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WomenProductVue",
  props: ["product"],
  data() {
    return {
      loading: false,
    };
  },
  methods: {
    nextProduct() {
      this.loading = true;
      this.$emit("next-product");
      // Setelah beberapa waktu (sebagai contoh, 2 detik), atur loading menjadi false
      setTimeout(() => {
        this.loading = false;
      }, 2000);
    },
  },
};
</script>


<style>
.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
.product {
  width: 100%;
  background-color: #fde2ff;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: linear-gradient(to bottom, #fde2ff 0%, #fde2ff 60%, #fff 60%, #Fff 100%);


}

.card {
  width: 900px; /* Lebar total dua kolom (col-md-6) */
  height: 400px;
  background-color: white;
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.image-container {
  height: 100%;
}

.image-container img {
  width: 400px;
  height: 500px;
  padding: 50px;
  object-fit: cover;
}

.text-container {
  padding: 16px;
  display: flex;
  flex-direction: column;
  padding: 35px 20px;
  /* justify-content: center; */
  align-items: flex-start; /* Mengubah alignment ke bagian awal container */
  height: 100%;
}
.category{
    display: flex;
}
.category .categoryContent{
    color: #3F3F3F;
}
.description{
    font-size: 20px;
    padding-bottom: 90px;
}
.pink{
    font-size: 28px;
    color: #720060;
}
.buy{
    width: 200px;
    background-color: #720060;
    color: white;
    font-weight: bold;
    margin-right: 20px;
}
.next{
    width: 200px;
    background-color: #ffffff;
    color: #720060;
    font-weight: bold;
}
</style>
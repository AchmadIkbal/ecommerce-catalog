<template>
  <div class="product1">
    <div v-if="loading" class="loader"></div>
    <div v-else class="card1">
      <div class="row">
        <div class="col-md-5">
          <div class="image-container1">
            <img :src="product.image" alt="" />
          </div>
        </div>
        <div class="col-md-7">
          <div class="text-container">
            <div>
              <h4 class="biru">{{ product.title }}</h4>
              <div class="category1">
                <p class="categoryContent1 col-md-6">{{ product.category }}</p>
                <div class="col-md-6 rating">
                  <span class="rating-circle">Rating: {{ product.rating.rate }}</span>
                </div>
              </div>
              <hr />
              <p class="description1">{{ product.description }}</p>
              <p class="biru">${{ product.price }}</p>
              
              <button class="buy1">Buy Now</button>
              <button class="next1" @click="nextProduct">
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
  name: "MenProduct",
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
.product1 {
  width: 100%;
  background-color: #002772;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: linear-gradient(to bottom, #002772 0%, #002772 60%, #fff 60%, #Fff 100%);


}

.card1 {
  width: 900px; /* Lebar total dua kolom (col-md-6) */
  height: 400px;
  background-color: white;
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.image-container1 {
  height: 100%;
}

.image-container1 img {
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
.category1 .categoryContent1{
    color: #3F3F3F;
}
.description1{
    font-size: 20px;
    padding-bottom: 90px;
}
.biru{
    font-size: 28px;
    color: #002772;
}
.buy1{
    width: 200px;
    background-color: #002772;
    color: white;
    font-weight: bold;
    margin-right: 20px;
}
.next1{
    width: 200px;
    background-color: #ffffff;
    color: #002772;
    font-weight: bold;
}
</style>
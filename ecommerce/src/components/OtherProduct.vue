<template>
  <div class="product2">
    <div v-if="loading" class="loader"></div>
    <div v-else class="card1">
      <div class="card-content">
        <div class="show">
          <h5>This Product Is Unavailable To Show</h5>
        </div>
        <button class="pageNext" @click="nextProduct">
          <span v-if="loading" class="loader"></span>
          <!-- Loader untuk tombol Next Product -->
          <span v-else>Next Product</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "OtherProduct",
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
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.product2 {
  width: 100%;
  background-color: #D8D7D7;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: linear-gradient(
    to bottom,
    #D8D7D7 0%,
    #D8D7D7 60%,
    #fff 60%,
    #fff 100%
  );
}

.card1 {
  width: 900px; /* Lebar total dua kolom (col-md-6) */
  height: 500px;
  background-color: white;
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.card-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%; /* Biarkan kontennya memenuhi tinggi kartu */
}

.pageNext {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 450px;
  background-color: #ffffff;
  color: #002772;
  font-weight: bold;
}

.show {
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

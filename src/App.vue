<template>
  <div class="app-wrapper">
    <AppHeader
      :productCategory="product?.category"
      @request-reset="resetToFirstProduct"
    />

    <main>
      <div :class="['product-card-container', cardClass]">
        <ProductCard
          :product="product || {}"
          :loading="loading"
          @request-next="nextProduct"
          @request-reset="resetToFirstProduct"
        />

        <div class="navigation-controls" v-if="!loading">
          <button @click="previousProduct" class="prev-product-btn">
            <span v-if="currentProductIndex === 1">
              Previous Product (Last)
            </span>
            <span v-else> Previous Product (ID: {{ prevIndex }}) </span>
          </button>

          <button @click="nextProduct">
            <span v-if="currentProductIndex === 20">
              Next Product (First)
            </span>
            <span v-else> Next Product (ID: {{ nextIndex }}) </span>
          </button>
        </div>
      </div>
    </main>

    <AppFooter :currentId="currentProductIndex" />
  </div>
</template>

<script>
import ProductCard from "./components/ProductCard.vue";
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  name: "App",
  components: {
    ProductCard,
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      currentProductIndex: 1,
      product: null,
      loading: false,
    };
  },
  computed: {
    nextIndex() {
      return this.currentProductIndex >= 20 ? 1 : this.currentProductIndex + 1;
    },
    prevIndex() {
      return this.currentProductIndex <= 1 ? 20 : this.currentProductIndex - 1;
    },
    cardClass() {
      if (this.loading || !this.product) {
        return "default-card-color";
      }

      const category = this.product.category;

      if (category === "men's clothing") {
        return "men-section";
      } else if (category === "women's clothing") {
        return "women-section";
      } else {
        return "unavailable-section";
      }
    },
  },
  methods: {
    async fetchProduct(index) {
      this.loading = true;
      this.product = null;

      const url = `https://fakestoreapi.com/products/${index}`;

      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        this.product = data;
      } catch (error) {
        console.error("Error fetching product:", error);
        this.product = {
          id: index,
          title: "Fetch Error",
          category: "error",
          description: "Gagal mengambil data dari API.",
        };
      } finally {
        this.loading = false;
      }
    },

    nextProduct() {
      let newIndex = this.currentProductIndex + 1;
      if (newIndex > 20) {
        newIndex = 1;
      }
      this.currentProductIndex = newIndex;
      this.fetchProduct(this.currentProductIndex);
    },

    previousProduct() {
      let newIndex = this.currentProductIndex - 1;
      if (newIndex < 1) {
        newIndex = 20;
      }
      this.currentProductIndex = newIndex;
      this.fetchProduct(this.currentProductIndex);
    },

    resetToFirstProduct() {
      this.currentProductIndex = 1;
      this.fetchProduct(this.currentProductIndex);
    },
  },
  mounted() {
    this.fetchProduct(this.currentProductIndex);
  },
};
</script>

<style>
/* --- BASE LAYOUT FOR STICKY HEADER/FOOTER --- */
.app-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
}

main {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  padding: 40px 20px;
}

/* --- Existing Styles for Product Card Container --- */
.product-card-container {
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: background-color 0.5s ease, border-color 0.5s ease;
  width: 100%;
  max-width: 800px;
}

/* Style untuk tombol navigasi */
.navigation-controls {
  margin-top: 25px;
  display: flex;
  justify-content: center; /* Kembali ke tengah */
  gap: 15px;
}

.navigation-controls button {
  /* Hapus kursor not-allowed dan warna abu-abu dari :disabled karena tombol hilang saat loading */
  padding: 15px 30px;
  border: none;
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
  background-color: var(--clr-dark-gray);
  color: white;
  font-size: 1.1em;
  transition: background-color 0.3s, transform 0.1s;
}

.navigation-controls .prev-product-btn {
  background-color: #5a6a78;
}

.navigation-controls button:hover {
  background-color: #2c3e50;
  transform: translateY(-2px);
}

/* --- Hapus styling disabled karena elemen akan hilang saat loading --- */
/* .navigation-controls button:disabled { ... } */

/* --- THEMES (Mengatur warna kontainer dan tombol aksi) --- */

.default-card-color {
  background-color: white;
  border: 1px solid #ccc;
}

.men-section {
  background-color: var(--clr-men-accent);
  border: 3px solid var(--clr-men-primary);
}
.men-section .product-title,
.men-section .product-price {
  color: var(--clr-men-primary);
}
.men-section .buy-now-btn {
  background-color: var(--clr-men-primary);
  color: white;
}
.men-section .buy-now-btn:hover {
  background-color: #005a8d;
}
.men-section .add-to-cart-btn {
  background-color: transparent;
  border: 2px solid var(--clr-men-primary);
  color: var(--clr-men-primary);
}
.men-section .add-to-cart-btn:hover {
  background-color: var(--clr-men-secondary);
  color: white;
}

.women-section {
  background-color: var(--clr-women-accent);
  border: 3px solid var(--clr-women-primary);
}
.women-section .product-title,
.women-section .product-price {
  color: var(--clr-women-primary);
}
.women-section .buy-now-btn {
  background-color: var(--clr-women-primary);
  color: white;
}
.women-section .buy-now-btn:hover {
  background-color: #c2185b;
}
.women-section .add-to-cart-btn {
  background-color: transparent;
  border: 2px solid var(--clr-women-primary);
  color: var(--clr-women-primary);
}
.women-section .add-to-cart-btn:hover {
  background-color: var(--clr-women-secondary);
  color: var(--clr-women-primary);
}

.unavailable-section {
  background-color: var(--clr-unavailable-secondary);
  border: 3px solid var(--clr-unavailable-primary);
}
</style>

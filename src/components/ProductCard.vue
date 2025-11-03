<template>
  <div class="product-card">
    <div v-if="loading" class="loading-state">Memuat Produk...</div>

    <div v-else>
      <div
        v-if="
          product.category === 'men\'s clothing' ||
          product.category === 'women\'s clothing'
        "
      >
        <div class="product-content">
          <div class="product-info">
            <h2 class="product-title">{{ product.title }}</h2>
            <p class="product-category">Kategori: {{ product.category }}</p>

            <div class="product-rating">
              <span class="rating-stars">{{
                generateStars(product.rating.rate)
              }}</span>
              <span class="rating-value">
                ({{ product.rating.rate.toFixed(1) }}/5)
              </span>
              <span class="rating-count">
                ({{ product.rating.count }} reviews)
              </span>
            </div>
          </div>

          <img
            :src="product.image"
            :alt="product.title"
            class="product-image"
            :class="{
              'img-men': product.category === 'men\'s clothing',
              'img-women': product.category === 'women\'s clothing',
            }"
          />

          <div class="product-details">
            <p class="product-price">${{ product.price.toFixed(2) }}</p>
            <p class="product-description">{{ product.description }}</p>
          </div>

          <div class="action-buttons">
            <button class="buy-now-btn">Beli Sekarang</button>
          </div>
        </div>
      </div>

      <div v-else class="unavailable-product-state">
        <div class="unavailable-content">
          <span class="unavailable-icon">🚫</span>
          <h3 class="unavailable-title">Produk Tidak Ditemukan</h3>
          <p class="unavailable-message-detail">
            Produk dengan ID {{ product.id }} (Kategori: {{ product.category }})
            tidak termasuk dalam kategori yang diizinkan saat ini.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    product: {
      type: Object,
      required: true,
    },
    loading: {
      type: Boolean,
      required: true,
    },
  },
  emits: ["request-next", "request-reset"],
  methods: {
    generateStars(rate) {
      const fullStars = Math.round(rate);
      const emptyStars = 5 - fullStars;
      const full = "★".repeat(fullStars);
      const empty = "☆".repeat(emptyStars);
      return full + empty;
    },
  },
};
</script>

<style scoped>
.product-image {
  width: 100%;
  max-width: 200px;
  height: auto;
  object-fit: contain;
  border-radius: 8px;
  padding: 15px;
  background-color: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
  transition: all 0.5s ease;
}

.img-men {
  border: 3px solid var(--clr-men-secondary);
}
.img-women {
  border: 3px solid var(--clr-women-secondary);
}

.product-card {
  min-height: 250px;
}
.product-content {
  display: grid;
  grid-template-columns: 2fr 4fr;
  gap: 20px;
  align-items: center;
}
.product-image {
  grid-row: 1 / span 4;
}
.product-info {
  grid-column: 2 / 3;
}
.product-details {
  grid-column: 2 / 3;
}
.action-buttons {
  grid-column: 2 / 3;
}

.product-title {
  font-size: 1.8em;
  margin-top: 0;
  margin-bottom: 5px;
}
.product-category {
  font-size: 0.9em;
  font-style: italic;
  margin-bottom: 5px;
}
.product-price {
  font-size: 2.5em;
  font-weight: bold;
  margin: 10px 0;
}
.product-description {
  font-size: 1em;
  color: var(--clr-text-secondary);
  line-height: 1.6;
}

.action-buttons {
  display: flex;
  gap: 15px;
  margin-top: 20px;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 15px;
  font-size: 1.1em;
}

.rating-stars {
  color: gold;
  letter-spacing: 2px;
}

.rating-value {
  font-weight: bold;
  color: var(--clr-text-primary);
}

.rating-count {
  font-size: 0.85em;
  color: var(--clr-text-secondary);
}

.loading-state,
.unavailable-product-state {
  text-align: center;
  min-height: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  font-size: 1.5em;
  color: var(--clr-text-secondary);
}
.unavailable-content {
  max-width: 400px;
  padding: 30px;
  border-radius: 10px;
  background-color: var(--clr-unavailable-secondary);
  border: 2px solid var(--clr-unavailable-primary);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
}
.unavailable-icon {
  font-size: 4em;
  display: block;
  margin-bottom: 10px;
}
.unavailable-title {
  font-size: 1.8em;
  color: var(--clr-unavailable-primary);
  margin-top: 0;
  margin-bottom: 5px;
}
.unavailable-message-detail {
  font-size: 1em;
  color: var(--clr-text-secondary);
  margin-bottom: 20px;
}
.unavailable-actions {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.unavailable-actions button {
  width: 100%;
  padding: 12px;
  font-weight: bold;
  border-radius: 6px;
  transition: background-color 0.3s;
}
.try-next-btn {
  background-color: var(--clr-unavailable-primary);
  color: white;
}
.try-next-btn:hover {
  background-color: #d84315;
}
.go-to-catalog-btn {
  background-color: white;
  border: 1px solid var(--clr-unavailable-primary);
  color: var(--clr-unavailable-primary);
}
.go-to-catalog-btn:hover {
  background-color: #f5f5f5;
}
</style>

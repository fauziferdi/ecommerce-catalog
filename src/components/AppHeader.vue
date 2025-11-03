<template>
  <header class="main-header">
    <nav class="navbar">
      <div class="nav-brand">Ecommerce Catalog</div>
      <div class="nav-links">
        <span @click="$emit('request-reset')" class="nav-link"
          >Home / Reset</span
        >
        <span class="nav-link nav-category"
          >Category: {{ productCategory || "Loading..." }}</span
        >
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    productCategory: {
      type: String,
      default: "N/A",
    },
  },
  emits: ["request-reset"],
};
</script>

<style scoped>
.main-header {
  width: 100%;
  background-color: var(--clr-dark-gray);
  color: white;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
}

.navbar {
  margin: 0 auto;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  font-size: 1.6em;
  font-weight: 700;
  color: var(--clr-light-gray);
}

.nav-links {
  display: flex;
  gap: 15px;
  font-size: 0.95em;
}

.nav-link {
  cursor: pointer;
  padding: 8px 12px;
  border-radius: 6px;
  transition: background-color 0.3s, color 0.3s;
  color: var(--clr-light-gray);
}

.nav-link:hover {
  background-color: #5a6a78;
}

.nav-category {
  font-style: italic;
  color: var(--clr-men-secondary);
  cursor: default;
}
</style>

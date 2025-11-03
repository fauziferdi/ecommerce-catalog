<template>
  <footer class="main-footer">
    <p>
      &copy; 2025 Product List | Current ID: {{ currentId }} | Ecommerce Catalog
    </p>
  </footer>
</template>

<script>
export default {
  name: "AppFooter",
  props: {
    currentId: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
/* --- FOOTER STYLES --- */
.main-footer {
  background-color: var(--clr-dark-gray);
  color: #b0b0b0;
  text-align: center;
  padding: 15px 20px;
  font-size: 0.85em;
}
</style>

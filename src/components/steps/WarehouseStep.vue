<template>
  <div class="step-content">
    <div class="container main-content py-5">
      <h1 class="main-title">Select Warehouse & Products :</h1>

      <div class="row g-4 mt-5">
        <div class="col-md-6">
          <div class="d-flex flex-column align-items-start">
            <label class="warehouse-label mb-1">From Warehouse:</label>
            <select class="form-select custom-select" v-model="fromWarehouse">
              <option value="roxa" :disabled="fromWarehouse === 'roxa'">
                Roxa
              </option>
              <option value="cairo" :disabled="fromWarehouse === 'cairo'">
                Cairo Warehouse
              </option>
              <option value="alex" :disabled="fromWarehouse === 'cairo'">
                Alexandria Warehouse
              </option>
            </select>
          </div>
        </div>

        <div class="col-md-6">
          <div class="d-flex flex-column align-items-start">
            <label class="warehouse-label mb-1">To Warehouse:</label>
            <select class="form-select custom-select" v-model="toWarehouse">
              <option value="dqq" :disabled="toWarehouse === 'dqq'">
                Dqq Warehouse
              </option>
              <option value="giza" :disabled="toWarehouse === 'giza'">
                Giza Warehouse
              </option>
              <option value="luxor" :disabled="toWarehouse === 'luxor'">
                Luxor Warehouse
              </option>
            </select>
          </div>
        </div>
      </div>

      <div class="products-section">
        <div class="section-header">
          <h2 class="section-title">Select Products</h2>
          <div class="position-relative">
            <img
              src="../../assets/search.png"
              alt="search-icon"
              class="search-icon"
            />
            <input
              type="text"
              class="search-box form-control ps-5"
              placeholder="Search"
              v-model="searchQuery"
            />
          </div>
        </div>

        <div class="row">
          <div
            class="col-md-6"
            v-for="product in filteredProducts"
            :key="product.id"
          >
            <ProductCard
              :product="product"
              @add="addProduct"
              @increase="increaseQuantity"
              @decrease="decreaseQuantity"
              @remove="removeProduct"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";

const fromWarehouse = ref("roxa");
const toWarehouse = ref("dqq");

import ProductCard from "@/components/warehouse-components/ProductCard.vue";
import debounce from "lodash.debounce";
import { PRODUCTS } from "@/assets/PRODUCTS";

const products = ref(PRODUCTS);

const searchQuery = ref("");
const debouncedQuery = ref("");

const updateDebounced = debounce((val) => {
  debouncedQuery.value = val;
}, 300);

watch(searchQuery, (val) => {
  updateDebounced(val);
});

const filteredProducts = computed(() => {
  if (!debouncedQuery.value) return products.value;
  return products.value.filter(
    (p) =>
      p.title.toLowerCase().includes(debouncedQuery.value.toLowerCase()) ||
      p.sku.toLowerCase().includes(debouncedQuery.value.toLowerCase())
  );
});

function addProduct(product) {
  product.quantity = 1;
}

function increaseQuantity(product) {
  if (product.quantity < product.stock) {
    product.quantity++;
  }
}

function decreaseQuantity(product) {
  if (product.quantity > 1) {
    product.quantity--;
  } else {
    product.quantity = 0;
  }
}

function removeProduct(product) {
  product.quantity = 0;
}
</script>

<style scoped>
.main-content {
  background: #24a2590a;
  border-radius: 1rem;
}

.main-title {
  text-align: start;
  color: #10b981;
  font-weight: 600;
  font-size: 1.5rem;
  margin-bottom: 2rem;
}

.warehouse-label {
  text-align: start;
  color: #10b981;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.custom-select {
  border: 2px solid #10b981;
  border-radius: 8px;
  font-size: 1rem;
  color: #6b7280;
  background-color: white;
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='%2310b981' viewBox='0 0 16 16'%3E%3Cpath d='M8 11L3 6h10l-5 5z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 1rem center;
  background-size: 16px;
  height: 3rem;
}

.custom-select:focus {
  outline: none;
  border-color: #059669;
  box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
}

.products-section {
  background-color: white;
  border-radius: 12px;
  padding: 2rem;
  margin-top: 2rem;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.section-title {
  color: #10b981;
  font-weight: 600;
  font-size: 1.3rem;
  margin: 0;
}

.search-box {
  background-color: #e0f2f1;
  border: none;
  border-radius: 8px;
  padding: 0.75rem 1rem 0.75rem 2.5rem;
  width: 300px;
  color: #10b981;
}

.search-box:focus {
  outline: none;
  background-color: #d1f0ed;
}

.search-icon {
  position: absolute;
  left: 12px;
  top: 50%;
  transform: translateY(-50%);
  width: 18px;
  height: 18px;
  pointer-events: none;
}
</style>

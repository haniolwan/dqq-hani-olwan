<template>
  <div class="product-card">
    <img :src="product.image" :alt="product.title" class="product-image" />

    <div class="product-info">
      <div class="product-title">{{ product.title }}</div>
      <div class="product-sku">SKU: {{ product.sku }}</div>
      <div class="product-stock">Stock : {{ product.stock }}</div>
    </div>

    <button
      v-if="!product.quantity"
      class="add-btn d-flex align-items-center gap-2"
      @click="$emit('add', product)"
    >
      <span>Add</span>
      <img src="../../assets/add.png" alt="add-icon" class="add-icon" />
    </button>

    <div v-else class="quantity-controls">
      <button class="qty-btn" @click="$emit('decrease', product)">-</button>
      <span class="quantity-box">{{ product.quantity }}</span>
      <button class="qty-btn" @click="$emit('increase', product)">+</button>
      <button class="remove-btn" @click="$emit('remove', product)">
        Remove
      </button>
    </div>
  </div>
</template>

<script setup>
/* global defineProps, defineEmits */
defineProps({ product: Object });
defineEmits(["add", "increase", "decrease", "remove"]);
</script>

<style scoped>
.product-card {
  background-color: #fafafa;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  transition: all 0.3s ease;
}

.product-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transform: translateY(-2px);
}

.product-image {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 8px;
  background-color: #f3e8e8;
}

.product-info {
  flex: 1;
}

.product-title {
  color: #374151;
  font-size: 0.95rem;
  margin-bottom: 0.5rem;
  text-align: start;
}

.product-sku {
  color: #9ca3af;
  font-size: 0.875rem;
  margin-bottom: 0.5rem;
}

.product-stock {
  color: #10b981;
  font-size: 0.875rem;
  font-weight: 500;
  border: 1px solid #10b981;
  border-radius: 9999px;
  background: #24a25914;
  padding: 6px 14px;
  display: inline-block;
}

.add-btn {
  background-color: white;
  border: 2px solid #10b981;
  color: #10b981;
  border-radius: 25px;
  padding: 0.5rem 1.5rem;
  font-weight: 500;
  transition: all 0.3s ease;
  cursor: pointer;
  gap: 10px;
}

.add-btn:hover {
  background-color: #10b981;
  color: white;
}

.add-icon {
  width: 18px;
  height: 18px;
}

.quantity-controls {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.qty-btn {
  background-color: white;
  border: 2px solid #10b981;
  color: #10b981;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  font-size: 1.2rem;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: all 0.2s ease;
}

.qty-btn:hover {
  background-color: #10b981;
  color: white;
}

.quantity-box {
  min-width: 40px;
  text-align: center;
  padding: 0.4rem 0.8rem;
  border: 2px solid #10b981;
  border-radius: 12px;
  font-weight: 600;
  color: #10b981;
  background-color: #e6f9f2;
}

.remove-btn {
  background-color: #fce7f3;
  border: none;
  color: #e11d48;
  padding: 0.5rem 1rem;
  border-radius: 25px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
}

.remove-btn:hover {
  background-color: #ff0037;
  color: white;
}
</style>

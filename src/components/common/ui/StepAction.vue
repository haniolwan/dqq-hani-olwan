<template>
  <div class="step-actions">
    <button
      v-if="showPrev"
      type="button"
      class="back-btn"
      @click="$emit('prev')"
    >
      <span class="arrow-icon">←</span>
      Previous
    </button>

    <button
      v-if="!isLast"
      type="button"
      class="submit-btn"
      @click="$emit('next')"
    >
      Next
    </button>

    <button v-else type="button" class="submit-btn" @click="$emit('submit')">
      Submit
    </button>
  </div>
</template>

<script setup>
// eslint-disable-next-line no-undef
defineProps({
  showPrev: { type: Boolean, default: true },
  isLast: { type: Boolean, default: false },
});

// eslint-disable-next-line no-undef
defineEmits(["prev", "next", "submit"]);
</script>

<style scoped>
.step-actions {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
  justify-content: center;
}

.back-btn {
  background-color: #e8f5e9;
  border: none;
  color: #10b981;
  padding: 1rem 2rem;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  min-width: 150px;
}

.back-btn:hover {
  background-color: #d4edd7;
  transform: translateX(-2px);
}

.back-btn:active {
  transform: scale(0.98);
}

.submit-btn {
  background-color: #10b981;
  border: none;
  color: white;
  padding: 1rem 2rem;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  min-width: 150px;
}

.submit-btn:hover {
  background-color: #059669;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
}

.submit-btn:active {
  transform: scale(0.98);
}

.arrow-icon {
  font-size: 1.2rem;
  font-weight: bold;
}
</style>

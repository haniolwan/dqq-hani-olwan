<template>
  <div class="step-content">
    <div class="form-container">
      <div class="form-group">
        <label class="form-label">Shipping Priority</label>
        <select class="custom-select" v-model="shippingPriority">
          <option value="high">High</option>
          <option value="medium">Medium</option>
          <option value="low">Low</option>
        </select>
      </div>

      <div class="form-group">
        <label class="form-label">Notes</label>
        <div class="textarea-wrapper">
          <textarea
            class="custom-textarea"
            placeholder="Write any notes..."
            v-model="notes"
            maxlength="500"
          ></textarea>
          <span class="char-counter">{{ charCount }}/500</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const shippingPriority = ref("high");
const notes = ref("");

const charCount = computed(() =>
  notes.value.length.toString().padStart(2, "0")
);
</script>

<style scoped>
.form-container {
  max-width: 1000px;
  margin: 0 auto;
  margin-top: 1rem;
}

.form-label {
  color: #10b981;
  font-weight: 700;
  font-size: 1.1rem;
  margin-bottom: 0.75rem;
}

.custom-select {
  border: 2px solid #10b981;
  border-radius: 8px;
  font-size: 1rem;
  color: #374151 !important;
  background-color: white;
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='%236b7280' viewBox='0 0 16 16'%3E%3Cpath d='M8 11L3 6h10l-5 5z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 1.25rem center;
  background-size: 16px;
  width: 100%;
}

.custom-select:focus {
  outline: none;
  border-color: #059669;
  box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
  color: #374151 !important;
}

.custom-select option {
  color: #374151 !important;
}

.custom-textarea {
  border: 2px solid #10b981;
  border-radius: 8px;
  padding: 1rem 1.25rem;
  font-size: 1rem;
  color: #374151;
  background-color: white;
  width: 100%;
  min-height: 150px;
  resize: vertical;
}

.custom-textarea::placeholder {
  color: #9ca3af;
}

.custom-textarea:focus {
  outline: none;
  border-color: #059669;
  box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
}

.textarea-wrapper {
  position: relative;
}

.char-counter {
  position: absolute;
  bottom: 1rem;
  right: 1.25rem;
  color: #9ca3af;
  font-size: 0.875rem;
  pointer-events: none;
}

.form-group {
  text-align: start;
  margin-bottom: 2rem;
}
</style>

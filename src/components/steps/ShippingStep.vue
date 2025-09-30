<template>
  <div class="step-content">
    <div class="container py-5">
      <div class="row g-3">
        <div
          v-for="option in shippingOptions"
          :key="option.id"
          class="col-md-4"
        >
          <div
            class="card h-100 position-relative"
            :class="
              selected === option.id ? 'border-success border-3' : 'border'
            "
            style="
              cursor: pointer;
              transition: all 0.3s ease;
              border-radius: 12px;
            "
            @click="selected = option.id"
          >
            <div
              class="card-body d-flex align-items-center justify-content-between p-4"
            >
              <div>
                <img
                  :src="option.logo"
                  :alt="option.id"
                  class="img-fluid"
                  style="
                    max-height: 60px;
                    max-width: 120px;
                    object-fit: contain;
                  "
                />
              </div>

              <div class="form-check" style="width: 24px; height: 24px">
                <input
                  v-model="selected"
                  class="form-check-input"
                  type="radio"
                  name="shipping"
                  :id="option.id"
                  :value="option.id"
                  style="width: 24px; height: 24px; cursor: pointer"
                  @click.stop
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import splLogo from "@/assets/spl.png";
import fedexLogo from "@/assets/fedex.png";
import smsaLogo from "@/assets/smsa.png";

const shippingOptions = [
  { id: "spl", logo: splLogo },
  { id: "fedex", logo: fedexLogo },
  { id: "smsa", logo: smsaLogo },
];

const selected = ref(null);
</script>

<style scoped>
.step-content {
  padding: 2rem;
}

.form-check-input:checked {
  background-color: #24a259; /* custom green */
  border-color: #24a259;
}

.form-check-input:focus {
  border-color: #24a259;
  box-shadow: 0 0 0 0.25rem rgba(36, 162, 89, 0.25);
}
</style>

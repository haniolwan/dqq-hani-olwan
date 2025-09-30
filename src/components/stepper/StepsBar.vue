<template>
  <div>
    <div ref="stepperEl" class="container mt-4 bs-stepper">
      <div class="bs-stepper-header" role="tablist">
        <template v-for="(step, index) in steps" :key="step.id">
          <div class="step" :data-target="`#${step.id}`">
            <button
              type="button"
              class="step-trigger"
              role="tab"
              :id="`${step.id}-trigger`"
            >
              <div class="icon-wrapper">
                <img :src="step.icon" :alt="step.title" />
              </div>
              <div class="bs-stepper-label">
                <span class="step-number">Step {{ index + 1 }}</span>
                <span class="step-title">{{ step.title }}</span>
              </div>
            </button>
          </div>
          <div v-if="index < steps.length - 1" class="line"></div>
        </template>
      </div>
      <div class="bs-stepper-content">
        <div
          id="shipping-part"
          class="content"
          role="tabpanel"
          aria-labelledby="shipping-part-trigger"
        >
          <ShippingStep />
          <div class="step-actions">
            <StepAction :showPrev="false" @next="next" />
          </div>
        </div>
        <div
          id="warehouse-part"
          class="content"
          role="tabpanel"
          aria-labelledby="warehouse-part-trigger"
        >
          <WarehouseStep />
          <div class="step-actions">
            <StepAction :showPrev="true" @prev="previous" @next="next" />
          </div>
        </div>
        <div
          id="settings-part"
          class="content"
          role="tabpanel"
          aria-labelledby="settings-part-trigger"
        >
          <SettingsStep />
          <div class="step-actions">
            <StepAction :showPrev="true" @prev="previous" @next="next" />
          </div>
        </div>
        <div
          id="review-part"
          class="content"
          role="tabpanel"
          aria-labelledby="review-part-trigger"
        >
          <ReviewStep />
          <div class="step-actions">
            <StepAction
              :showPrev="true"
              :isLast="true"
              @prev="previous"
              @submit="submit"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import Stepper from "bs-stepper";
import "bs-stepper/dist/css/bs-stepper.min.css";
import ShippingStep from "./steps/ShippingStep.vue";
import WarehouseStep from "./steps/WarehouseStep.vue";
import SettingsStep from "./steps/SettingsStep.vue";
import ReviewStep from "./steps/ReviewStep.vue";
import StepAction from "../common/ui/StepAction.vue";

const stepperEl = ref(null);
let stepper = null;

const steps = [
  {
    id: "shipping-part",
    title: "Shipping Company",
    icon: new URL("../../assets/elements.png", import.meta.url).href,
  },
  {
    id: "warehouse-part",
    title: "Warehouses & Products",
    icon: new URL("../../assets/warehouse.png", import.meta.url).href,
  },
  {
    id: "settings-part",
    title: "Settings",
    icon: new URL("../../assets/settings.png", import.meta.url).href,
  },
  {
    id: "review-part",
    title: "Review",
    icon: new URL("../../assets/review.png", import.meta.url).href,
  },
];

onMounted(() => {
  stepper = new Stepper(stepperEl.value, {
    linear: false,
  });
});

onBeforeUnmount(() => {
  stepper = null;
});

const highlightCompleted = (index) => {
  // highlight completed step
  const stepsEl = stepperEl.value.querySelectorAll(".step");
  if (stepsEl[index]) {
    stepsEl[index].classList.add("completed");
  }
};

const next = () => {
  const currentIndex = stepper._currentIndex;
  highlightCompleted(currentIndex);
  stepper?.next();
};

const previous = () => {
  stepper?.previous();
  const currentIndex = stepper._currentIndex;
  const stepsEl = stepperEl.value.querySelectorAll(".step");
  if (stepsEl[currentIndex]) {
    stepsEl[currentIndex].classList.remove("completed");
  }
};

const submit = () => {
  alert("Form submitted!");
};
</script>

<style scoped>
.icon-wrapper {
  background-color: #22303e40;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.5rem;
  transition: background-color 0.3s ease;
}

.icon-wrapper img {
  width: 24px;
  height: 24px;
}

:deep(.bs-stepper .step.active) .icon-wrapper {
  background-color: #24a259;
}

:deep(.bs-stepper .step.active) .step-title {
  color: #24a259;
}

:deep(.bs-stepper .step.completed) .icon-wrapper {
  background-color: #24a259;
}

:deep(.bs-stepper .step.completed) .step-title {
  color: #24a259;
}

.bs-stepper-label {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.step-number {
  font-size: 0.9rem;
  color: #666;
  transition: color 0.3s ease;
}

.step-title {
  font-size: 1.1rem;
  font-weight: 500;
  color: #333;
  transition: color 0.3s ease;
}

.content {
  padding: 0;
}

.step-actions {
  padding: 0 2rem 2rem;
}

.btn {
  padding: 0.5rem 1.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  margin-right: 0.5rem;
}

.btn-next,
.btn-submit {
  background-color: #24a259;
  color: white;
}

.btn-prev {
  background-color: #6c757d;
  color: white;
}

.btn:hover {
  opacity: 0.9;
}
</style>

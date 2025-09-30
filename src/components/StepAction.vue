<template>
  <div class="step-actions">
    <button
      v-if="showPrev"
      type="button"
      class="btn btn-secondary me-2"
      @click="$emit('prev')"
    >
      Previous
    </button>

    <button
      v-if="!isLast"
      type="button"
      class="btn btn-success"
      @click="$emit('next')"
    >
      Next
    </button>

    <button
      v-else
      type="button"
      class="btn btn-success"
      @click="$emit('submit')"
    >
      Submit
    </button>
  </div>
</template>
<script>
export default {
  props: {
    showPrev: { type: Boolean, default: true },
    isLast: { type: Boolean, default: false },
  },
  emits: ["prev", "next", "submit"],
};
</script>

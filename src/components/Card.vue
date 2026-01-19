<script setup>
defineProps({
  hoverable: {
    type: Boolean,
    default: true
  },
  active: {
    type: Boolean,
    default: false
  },
  noPadding: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <div
      class="card"
      :class="{
      'is-hoverable': hoverable,
      'is-active': active,
      'has-padding': !noPadding
    }"
  >
    <slot></slot>
  </div>
</template>

<style scoped>
.card {
  background-color: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  transition: all 0.2s ease-in-out;
  position: relative;
  overflow: hidden;
}

.card.has-padding {
  padding: 16px;
}

.card.is-hoverable:hover {
  border-color: #cbd5e1;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); /* Đổ bóng */
  transform: translateY(-2px);
}

.card.is-active {
  background-color: #f0fdf4;
  border-color: #86efac;
}
</style>
<script setup>
import {computed} from 'vue'
import {COURSE_ICONS} from "../constant/COURSE_ICONS.js";

const props = defineProps({
  code: String,
  name: String,
  credits: [Number, String],
  modelValue: Boolean,
  icon: {
    type: String,
    default: 'shield'
  }
})

// Code bây giờ rất ngắn gọn
const currentIconRaw = computed(() => COURSE_ICONS[props.icon] || COURSE_ICONS['shield'])
</script>

<template>
  <div
      class="course-card"
      :class="{ 'is-completed': modelValue }"
  >
    <div class="card-left" :class="{ 'is-completed': modelValue }">
      <div class="checkbox-box">
        <svg v-if="modelValue" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
             stroke-width="4" stroke-linecap="round" stroke-linejoin="round" class="check-icon">
          <polyline points="20 6 9 17 4 12"></polyline>
        </svg>
      </div>
    </div>

    <div class="card-right" :class="{ 'is-completed': modelValue }">

      <div
          class="shield-icon"
          v-html="currentIconRaw"
      ></div>
      <div class="text-content">
        <div class="course-title">
          {{ code }} - {{ name }} - {{ credits }} TC
        </div>
      </div>

    </div>
  </div>
</template>

<style scoped>
.course-card {
  display: flex;
  width: 100%;
  border-radius: 8px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.2s ease;
  user-select: none;
  margin-bottom: 8px;
  color: #1d1d1d
}

.course-card:hover {
  transform: translateY(-1px);
}

.course-card.is-completed {
  color: #f4fef7;
}

.card-left {
  width: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #eaeceb;
}

.card-left.is-completed {
  background-color: #d1e8d1;
}

.checkbox-box {
  width: 20px;
  height: 20px;
  border: 2px solid #bbbdbc;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
}

.is-completed .checkbox-box {
  border: none !important;
  background-color: #4b9c50;
}

.check-icon {
  width: 14px;
  height: 14px;
  color: white;
}

.card-right {
  flex: 1;
  padding: 12px;
  display: flex;
  align-items: center;
  gap: 12px;
  border-radius: 8px;
  margin-left: -8px;
  z-index: 1;
  background-color: #cbcbcb;
}

.card-right.is-completed {
  background-color: #4b9c50;
}

.shield-icon svg {
  width: 24px;
  height: 24px;
  color: #1d1d1d;
}

.is-completed .shield-icon svg {
  color: #f4fef7;
}

.text-content {
  display: flex;
  flex-direction: column;
}

.course-title {
  font-weight: 600;
  font-size: 15px;
}
</style>
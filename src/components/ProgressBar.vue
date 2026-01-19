<template>
  <div class="progress-wrapper">
    <div class="progress-track">
      <div class="remaining-credits">
        Còn lại: {{ total - current }} TC
      </div>
      <div
          class="progress-fill bg-green"
          :style="{ width: percentage + '%' }">
        <div class="current-credits">
          Đã tích lũy: {{ current }} TC
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {computed} from 'vue'

const props = defineProps({
  current: {
    type: Number,
    required: true
  },
  total: {
    type: Number,
    default: 60
  },
})

const percentage = computed(() => {
  if (props.total === 0) return 0
  return Math.round((props.current / props.total) * 100)
})

</script>

<style scoped>
.progress-wrapper {
  width: 100%;
}

.progress-track {
  position: relative;
  height: 2.4rem;
  background-color: #cdcdcb;
  border-radius: 99px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  align-items: center;

  .current-credits {
    margin-left: 30px;
    text-transform: uppercase;
    color: white;
  }
}

.bg-green {
  background-color: #4ca153;
}

.remaining-credits {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  white-space: nowrap;
  text-transform: uppercase;
}
</style>
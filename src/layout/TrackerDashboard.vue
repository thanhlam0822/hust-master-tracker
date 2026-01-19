<template>
  <div class="container">
    <div class="title">
      Bảng theo dõi tiến độ học tập - thạc sĩ CNTT (HUST)
    </div>
    <div class="sum-progress">
      <card>
        <p class="title">Tổng tiến độ: 60 tín chỉ</p>
        <div class="progress-bar">
          <progress-bar :current="10" :total="60"/>
        </div>
      </card>
    </div>
  </div>
</template>
<script setup lang="ts">

import Card from "../components/Card.vue";
import ProgressBar from "../components/ProgressBar.vue";
</script>
<style scoped lang="scss">
.container {
  width: 100vw;
  height: 100vh;
  background: #e9edf0;
  padding: 0 20px;
}

.title {
  text-transform: uppercase;
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  padding-top: 20px;
}

.sum-progress {
  margin-top: 20px;

  .title {
    font-size: 1.4rem;
    padding-top: 0 !important;
  }

  .progress-bar {
    margin-top: 10px;
  }
}

</style>
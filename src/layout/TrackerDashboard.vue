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
    <div class="subjects">
      <div>
        <card>
          <p class="common-title">Khối kiến thức chung (3 TC)</p>
          <div class="course-list grid-cols-2">
            <course-item
                v-for="course in generalKnowledgeBlock"
                :key="course.id"
                :code="course.code"
                :name="course.name"
                :credits="course.credit"
                :icon="course.icon"
                v-model="course.done"
            />
          </div>
        </card>
        <card>
          <p class="common-title">Khối kiến thức ngành rộng (12 TC)</p>
          <div class="course-list grid-cols-2">
            <course-item
                v-for="course in broadDisciplinaryKnowledgeBlock"
                :key="course.id"
                :code="course.code"
                :name="course.name"
                :credits="course.credit"
                :icon="course.icon"
                v-model="course.done"
            />
          </div>
        </card>
      </div>
      <div>
        <card>
          <p class="common-title">Khối kiến thức ngành rộng (12 TC)</p>
          <div class="course-list">
            <course-item
                v-for="course in broadDisciplinaryKnowledgeBlock"
                :key="course.id"
                :code="course.code"
                :name="course.name"
                :credits="course.credit"
                :icon="course.icon"
                v-model="course.done"
            />
          </div>
        </card>
      </div>
      <div>
        <card>
          <p class="common-title">Khối kiến thức ngành rộng (12 TC)</p>
          <div class="course-list grid-cols-3">
            <course-item
                v-for="course in broadDisciplinaryKnowledgeBlock"
                :key="course.id"
                :code="course.code"
                :name="course.name"
                :credits="course.credit"
                :icon="course.icon"
                v-model="course.done"
            />
          </div>
        </card>
        <card>
          <p class="common-title">Khối kiến thức ngành rộng (12 TC)</p>
          <div class="course-list grid-cols-3">
            <course-item
                v-for="course in broadDisciplinaryKnowledgeBlock"
                :key="course.id"
                :code="course.code"
                :name="course.name"
                :credits="course.credit"
                :icon="course.icon"
                v-model="course.done"
            />
          </div>
        </card>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import {ref} from "vue";
import Card from "../components/Card.vue";
import ProgressBar from "../components/ProgressBar.vue";
import CourseItem from "../components/CourseItem.vue";

const generalKnowledgeBlock = ref([
  {id: 1, code: 'SS6010', name: 'Triết học', credit: 3, done: true, icon: 'shield_check'},
])

const broadDisciplinaryKnowledgeBlock = ref([
  {id: 2, code: 'IT6460', name: 'Quản trị dự án CNTT và quản lý thay đổi', credit: 2, icon: 'briefcase'},
  {id: 3, code: 'IT4818', name: 'Phân tích nghiệp vụ thông minh', credit: 2, icon: 'network'},
  {id: 4, code: 'IT6820', name: 'Kiến trúc máy tính tiên tiến', credit: 2, icon: 'cpu'},
  {id: 5, code: 'IT6819', name: 'Kiến trúc phần mềm', credit: 2, icon: 'codesandbox'},
  {id: 6, code: 'IT6340', name: 'Các hệ thống thông minh', credit: 2, icon: 'brain'},
  {id: 7, code: 'IT5440', name: 'Nguyên lý và kỹ thuật phân tích chương trình', credit: 2, icon: 'document'}
])
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
  color: #0e0e0e;
}

.sum-progress {
  margin-top: 20px;

  .title {
    font-size: 1.4rem;
    padding-top: 0 !important;
    color: #020202;
  }

  .progress-bar {
    margin-top: 10px;
  }
}

.subjects {
  display: flex;
  justify-content: space-between;
  gap: 10px;

  .common-title {
    font-size: 1.1rem;
    color: #0e0e0e;
    font-weight: bold;
    text-transform: uppercase;
  }

  .course-list {
    margin-top: 10px;
    display: grid;
    gap: 16px;
  }
}

:deep(.card) {
  margin-top: 10px !important;
}


.grid-cols-1 {
  grid-template-columns: 1fr;
}

.grid-cols-2 {
  grid-template-columns: repeat(2, 1fr);
}

.grid-cols-3 {
  grid-template-columns: repeat(3, 1fr);
}
</style>
<template>
  <div class="container">
    <div class="title">
      Bảng theo dõi tiến độ học tập - thạc sĩ CNTT (HUST)
    </div>
    <div class="sum-progress">
      <card>
        <p class="title">Tổng tiến độ: {{ totalCredit }} tín chỉ</p>
        <div class="progress-bar">
          <progress-bar :current="currentCredit" :total="totalCredit"/>
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
        <card class="expand-card">
          <p class="common-title">Khối kiến thức ngành rộng ({{ broadDisciplinaryKnowledgeCredits }} TC)</p>
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
          <p class="common-title">Khối kiến thức chuyên ngành nâng cao ({{ advancedSpecializedKnowledgeCredits }}TC)</p>
          <div class="course-list">
            <course-item
                v-for="course in advancedSpecializedKnowledgeBlock"
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
          <p class="common-title">Khối mô-đun định hướng ứng dụng ({{ applicationOrientedModuleCredits }}TC) - Chọn
            1</p>
          <div class="custom-course-list-container no-bottom-border">
            <div class="custom-title">
              LỰA CHỌN A: Công nghệ phần mềm
            </div>
            <div class="course-list no-margin-top grid-cols-3">
              <course-item
                  v-for="course in applicationOrientedModuleBlock.optionA"
                  :key="course.id"
                  :code="course.code"
                  :name="course.name"
                  :credits="course.credit"
                  :icon="course.icon"
                  v-model="course.done"
              />
            </div>
          </div>

          <div class="custom-course-list-container no-margin-top">
            <div class="custom-title">
              LỰA CHỌN B: Hệ thống thông tin
            </div>
            <div class="course-list no-margin-top grid-cols-3">
              <course-item
                  v-for="course in applicationOrientedModuleBlock.optionB"
                  :key="course.id"
                  :code="course.code"
                  :name="course.name"
                  :credits="course.credit"
                  :icon="course.icon"
                  v-model="course.done"
              />
            </div>
            <div class="note">
              Lưu ý: Chọn 1 trong 2 mô đun và hoàn thành toàn bộ các môn trong mô đun đã chọn
            </div>
          </div>
        </card>
        <card class="expand-card">
          <p class="common-title">Thực tập và luận văn tốt nghiệp ({{ graduateSubjectCredits }} TC)</p>
          <div class="course-list grid-cols-3">
            <course-item
                v-for="course in graduationInternshipAndGraduationThesis"
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
import {ref, computed} from "vue";
import Card from "../components/Card.vue";
import ProgressBar from "../components/ProgressBar.vue";
import CourseItem from "../components/CourseItem.vue";

const generalKnowledgeBlock = ref([
  {id: 1, code: 'SS6013', name: 'Triết học', credit: 3, icon: 'shield_check', done: true},
])

const broadDisciplinaryKnowledgeBlock = ref([
  {id: 2, code: 'IT6460', name: 'Quản trị dự án CNTT và quản lý thay đổi', credit: 2, icon: 'briefcase'},
  {id: 3, code: 'IT4818', name: 'Phân tích nghiệp vụ thông minh', credit: 2, icon: 'network'},
  {id: 4, code: 'IT6820', name: 'Kiến trúc máy tính tiên tiến', credit: 2, icon: 'cpu'},
  {id: 5, code: 'IT6819', name: 'Kiến trúc phần mềm', credit: 2, icon: 'codesandbox', done: true},
  {id: 6, code: 'IT6340', name: 'Các hệ thống thông minh', credit: 2, icon: 'brain', done: true},
  {id: 7, code: 'IT5440', name: 'Nguyên lý và kỹ thuật phân tích chương trình', credit: 2, icon: 'document'}
])

const advancedSpecializedKnowledgeBlock = ref([
  {id: 8, code: 'IT4922', name: 'Mạng thế hệ sau', credit: 2, icon: 'network', done: true},
  {id: 9, code: 'IT4527', name: 'Blockchain và ứng dụng', credit: 2, icon: 'coin', done: true},
  {id: 10, code: 'IT4772', name: 'Xử lý ngôn ngữ tự nhiên', credit: 3, icon: 'brain'},
  {id: 11, code: 'IT5419', name: 'Tích hợp hệ thống thông tin', credit: 3, icon: 'network'},
  {id: 12, code: 'IT6390', name: 'Web ngữ nghĩa', credit: 3, icon: 'globe'},
  {id: 13, code: 'IT4235', name: 'Thị giác máy tính', credit: 2, icon: 'scan_eye'},
  {id: 14, code: 'IT5550', name: 'Các giải pháp và chính sách an ninh mạng', credit: 3, icon: 'graduate', done: true}
])

const applicationOrientedModuleBlock = ref({
  optionA: [
    {id: 15, code: 'IT6575', name: 'Nguyên lý và mô thức phát triển hệ phân tán', credit: 2, icon: 'book'},
    {id: 16, code: 'IT5404', name: 'Điện toán đám mây', credit: 3, icon: 'cloud', done: true},
    {id: 17, code: 'IT6490', name: 'Các phương pháp Agile', credit: 2, icon: 'square_chart_gantt', done: true},
    {id: 18, code: 'IT6818', name: 'Mô hình hóa và phân tích phần mềm', credit: 3, icon: 'folder_code', done: true},
    {id: 19, code: 'IT6072', name: 'An toàn hệ thống thông tin', credit: 2, icon: 'shield_plus'},
  ],
  optionB: [
    {id: 20, code: 'IT6575', name: 'Nguyên lý và mô thức phát triển hệ phân tán', credit: 2, icon: 'book'},
    {id: 21, code: 'IT5408', name: 'Tính toán hiệu năng cao', credit: 2, icon: 'chart_no_axes_combined'},
    {id: 22, code: 'IT5404', name: 'Điện toán đám mây', credit: 3, icon: 'cloud'},
    {id: 23, code: 'IT5420', name: 'Tích hợp dữ liệu', credit: 3, icon: 'database'},
    {id: 24, code: 'IT5429', name: 'Phân tích đồ thị với dữ liệu lớn', credit: 2, icon: 'chart_spline'},
  ]
})

const graduationInternshipAndGraduationThesis = ref([
  {id: 25, code: 'TT6000', name: 'Thực tập tốt nghiệp thạc sĩ', credit: 6, icon: 'briefcase', done: true},
  {id: 26, code: 'LV6002', name: 'Luận văn tốt nghiệp thạc sĩ', credit: 9, icon: 'scroll_text'},
])

const broadDisciplinaryKnowledgeCredits = computed(() =>
    broadDisciplinaryKnowledgeBlock.value.reduce(
        (sum, c) => sum + c.credit,
        0
    )
)

const advancedSpecializedKnowledgeCredits = computed(() =>
    advancedSpecializedKnowledgeBlock.value.reduce(
        (sum, c) => sum + c.credit,
        0
    )
)

const applicationOrientedModuleCredits = computed(() =>
    applicationOrientedModuleBlock.value.optionA.reduce(
        (sum, c) => sum + c.credit,
        0
    )
)

const graduateSubjectCredits = computed(() =>
    graduationInternshipAndGraduationThesis.value.reduce(
        (sum, c) => sum + c.credit,
        0
    )
)

const totalCredit = computed(() =>
    broadDisciplinaryKnowledgeCredits.value
    + advancedSpecializedKnowledgeCredits.value
    + applicationOrientedModuleCredits.value
    + graduateSubjectCredits.value
    + 3
)

const countDone = (courses = []) =>
    courses
        .filter(c => c.done)
        .reduce((sum, c) => sum + c.credit, 0)

const currentCredit = computed(() => {
  return (
      countDone(generalKnowledgeBlock.value) +
      countDone(broadDisciplinaryKnowledgeBlock.value) +
      countDone(advancedSpecializedKnowledgeBlock.value) +
      countDone(
          applicationOrientedModuleBlock.value.optionA
      ) +
      countDone(graduationInternshipAndGraduationThesis.value)
  )
})
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
    align-items: stretch;
  }

  .custom-title {
    padding: 8px 0;
    font-weight: bold;
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

.custom-course-list-container {
  width: 100%;
  border: 2px dashed #d3d3d3;
  padding: 0 20px 10px 20px;
  margin-top: 10px;
}

.custom-course-list-container.no-bottom-border {
  border-bottom: none;
}

.no-margin-top {
  margin-top: 0 !important;
}

.note {
  font-style: italic;
}

.course-list :deep(.course-card) {
  height: 70px;
}

.subjects {
  display: flex;
  gap: 10px;

  > div {
    display: flex;
    flex-direction: column;
    min-height: 0;
  }
}

.expand-card {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  min-height: 0;
}
</style>
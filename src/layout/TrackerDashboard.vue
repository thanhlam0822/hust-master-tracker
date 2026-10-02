<template>
  <div class="hust-dashboard">
    <header class="hust-header">
      <div class="header-left">
        <div>
          <img src="../assets/logo_hust.webp" alt="HUST Logo" width="55" height="65"/>
        </div>
        <h1 class="header-title">HỆ THỐNG QUẢN LÝ VÀ THEO DÕI TIẾN ĐỘ HỌC TẬP - THẠC SĨ CNTT (HUST)</h1>
      </div>
      <div class="header-right">
        <img class="logo-en" src="../assets/logo_hust_en.png" alt="HUST Logo"/>
      </div>
    </header>

    <main class="dashboard-body">
      <section class="top-cards-grid">
        <div class="card stat-card">
          <div class="card-title">TỔNG TÍN CHỈ TÍCH LŨY</div>
          <div class="stat-main">
            <div class="stat-number">{{ currentCredit }}/{{ totalCredit }} TC</div>
            <div class="stat-sub font-bold">{{ progressPercentage }}%</div>
          </div>
          <div class="progress-bar-container">
            <div class="progress-bar-fill" :style="{ width: progressPercentage + '%' }"></div>
          </div>
        </div>

        <div class="card stat-card">
          <div class="card-title">ĐIỂM TRUNG BÌNH HỆ 4</div>
          <div class="stat-main">
            <div class="stat-number text-large">{{ currentCPA.toFixed(2) }}</div>
          </div>
        </div>

        <div class="card stat-card">
          <div class="card-title">LẬP KẾ HOẠCH CPA MỤC TIÊU</div>
          <div class="input-group">
            <input
                type="text"
                v-model="targetCPA"
                placeholder="Nhập CPA Mục Tiêu (ví dụ: 3.50)"
                class="custom-input"
            />
          </div>
          <button class="btn-calculate">TÍNH TOÁN KẾ HOẠCH</button>
        </div>


        <div class="card stat-card table-card-compact">
          <div class="card-title px-10">BẢNG ĐIỂM CẦN ĐẠT</div>
          <table class="pure-table compact-table">
            <thead>
            <tr>
              <th style="width: 35%;">Mã Môn</th>
              <th style="width: 35%;">Tín chỉ</th>
              <th style="width: 30%;" class="text-right">Điểm Chữ</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="item in targetScores" :key="item.code">
              <td>{{ item.code }}</td>
              <td>{{ item.credit }} TTC</td>
              <td class="text-right font-medium">{{ item.target }}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </section>

      <section class="main-columns-grid">
        <div class="column-col">
          <div class="card table-card">
            <div class="table-header-title">Khối kiến thức chung (3 TC)</div>
            <table class="pure-table">
              <thead>
              <tr>
                <th style="width: 22%;">Mã Môn</th>
                <th>Tên Môn Học</th>
                <th style="width: 18%;">Tín Chỉ (TC)</th>
                <th style="width: 18%;">Điểm Số (ĐTB)</th>
                <th style="width: 15%;">Điểm Chữ</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="course in generalBlock" :key="course.id">
                <td class="font-medium">{{ course.code }}</td>
                <td>{{ course.name }}</td>
                <td>{{ course.credit }} TC</td>
                <td>{{ course.score !== undefined ? course.score.toFixed(1) : '-' }}</td>
                <td class="font-bold">{{ course.grade || '-' }}</td>
              </tr>
              </tbody>
            </table>
          </div>

          <div class="card table-card">
            <div class="table-header-title">Khối kiến thức ngành rộng (12 TC)</div>
            <table class="pure-table">
              <thead>
              <tr>
                <th style="width: 22%;">Mã Môn</th>
                <th>Tên Môn Học</th>
                <th style="width: 18%;">Tín Chỉ</th>
                <th style="width: 18%;">Điểm (ĐTB)</th>
                <th style="width: 15%;">Điểm Chữ</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="course in broadBlock" :key="course.id">
                <td class="font-medium">{{ course.code }}</td>
                <td>{{ course.name }}</td>
                <td>{{ course.credit }} TC</td>
                <td>{{ course.score !== undefined ? course.score.toFixed(1) : '-' }}</td>
                <td class="font-bold">{{ course.grade || '-' }}</td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="column-col">
          <div class="card table-card h-full">
            <div class="table-header-title">Khối kiến thức chuyên ngành nâng cao (18TC)</div>
            <table class="pure-table">
              <thead>
              <tr>
                <th style="width: 22%;">Mã Môn</th>
                <th>Tên Môn Học</th>
                <th style="width: 20%;">Điểm Số (ĐTB)</th>
                <th style="width: 18%;">Điểm Chữ</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="course in advancedBlock" :key="course.id">
                <td class="font-medium">{{ course.code }}</td>
                <td>{{ course.name }}</td>
                <td>{{ course.score !== undefined ? course.score.toFixed(1) : '-' }}</td>
                <td class="font-bold">{{ course.grade || '-' }}</td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="column-col">
          <div class="card table-card">
            <div class="table-header-title">Khối mô-đun định hướng ứng dụng (12TC) - Chọn 1</div>
            <div class="tabs-header">
              <button
                  class="tab-btn"
                  :class="{ active: currentTab === 'A' }"
                  @click="currentTab = 'A'"
              >
                LỰA CHỌN A: Công nghệ phần mềm
              </button>
              <button
                  class="tab-btn"
                  :class="{ active: currentTab === 'B' }"
                  @click="currentTab = 'B'"
              >
                LỰA CHỌN B: Hệ thống thông tin
              </button>
            </div>

            <table class="pure-table">
              <thead>
              <tr>
                <th style="width: 20%;">Mã Môn</th>
                <th>Tên Môn Học</th>
                <th style="width: 18%;">Tín Chỉ</th>
                <th style="width: 18%;">Điểm Số (ĐTB)</th>
                <th style="width: 15%;">Điểm Chữ</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="course in (currentTab === 'A' ? applicationBlock.optionA : applicationBlock.optionB)"
                  :key="course.id">
                <td class="font-medium">{{ course.code }}</td>
                <td>{{ course.name }}</td>
                <td>{{ course.credit }} TC</td>
                <td>{{ course.score !== undefined ? course.score.toFixed(1) : '-' }}</td>
                <td class="font-bold">{{ course.grade || '-' }}</td>
              </tr>
              </tbody>
            </table>
          </div>

          <div class="card table-card">
            <div class="table-header-title">Thực tập và luận văn tốt nghiệp (15 TC)</div>
            <table class="pure-table">
              <thead>
              <tr>
                <th style="width: 20%;">Mã Môn</th>
                <th>Tên Môn Học</th>
                <th style="width: 18%;">Tín Chỉ</th>
                <th style="width: 18%;">Điểm (ĐTB)</th>
                <th style="width: 15%;">Điểm Chữ</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="course in graduationBlock" :key="course.id">
                <td class="font-medium">{{ course.code }}</td>
                <td>{{ course.name }}</td>
                <td>{{ course.credit }} TC</td>
                <td>{{ course.score !== undefined ? course.score.toFixed(1) : '-' }}</td>
                <td class="font-bold">{{ course.grade || '-' }}</td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup lang="ts">
import {ref, computed, onMounted} from 'vue'

const hustRegistrationData = ref<any[]>([])
const currentTab = ref<'A' | 'B'>('A')
const targetCPA = ref('')
const currentCPA = ref(3.25)
const totalCredit = ref(60)
const currentCredit = ref(49)

const progressPercentage = computed(() => {
  return Math.round((currentCredit.value / totalCredit.value) * 100)
})

const targetScores = ref([
  {code: 'IT5440', credit: 2, target: '7.0/10'},
  {code: 'IT5400', credit: 2, target: '7.0/10'},
  {code: 'LV6002', credit: 2, target: '8.5/10'}
])

const generalBlock = ref([
  {id: 1, code: 'SS6013', name: 'Triết học', credit: 3, icon: 'shield_check'},
])

const broadBlock = ref([
  {id: 2, code: 'IT6460', name: 'Quản trị dự án CNTT và quản lý thay đổi', credit: 2, icon: 'briefcase'},
  {id: 3, code: 'IT4818', name: 'Phân tích nghiệp vụ thông minh', credit: 2, icon: 'network'},
  {id: 4, code: 'IT6820', name: 'Kiến trúc máy tính tiên tiến', credit: 2, icon: 'cpu'},
  {id: 5, code: 'IT6819', name: 'Kiến trúc phần mềm', credit: 2, icon: 'codesandbox'},
  {id: 6, code: 'IT6340', name: 'Các hệ thống thông minh', credit: 2, icon: 'brain'},
  {id: 7, code: 'IT5440', name: 'Nguyên lý và kỹ thuật phân tích chương trình', credit: 2, icon: 'document'}
])

const advancedBlock = ref([
  {id: 8, code: 'IT4922', name: 'Mạng thế hệ sau', credit: 2, icon: 'network'},
  {id: 9, code: 'IT4527', name: 'Blockchain và ứng dụng', credit: 2, icon: 'coin'},
  {id: 10, code: 'IT4772', name: 'Xử lý ngôn ngữ tự nhiên', credit: 3, icon: 'brain'},
  {id: 11, code: 'IT5419', name: 'Tích hợp hệ thống thông tin', credit: 3, icon: 'network'},
  {id: 12, code: 'IT6390', name: 'Web ngữ nghĩa', credit: 3, icon: 'globe'},
  {id: 13, code: 'IT4235', name: 'Thị giác máy tính', credit: 2, icon: 'scan_eye'},
  {id: 14, code: 'IT5550', name: 'Các giải pháp và chính sách an ninh mạng', credit: 3, icon: 'graduate'}
])

const applicationBlock = ref({
  optionA: [
    {id: 15, code: 'IT6575', name: 'Nguyên lý và mô thức phát triển hệ phân tán', credit: 2, icon: 'book'},
    {id: 16, code: 'IT5404', name: 'Điện toán đám mây', credit: 3, icon: 'cloud'},
    {id: 17, code: 'IT6490', name: 'Các phương pháp Agile', credit: 2, icon: 'square_chart_gantt'},
    {id: 18, code: 'IT6818', name: 'Mô hình hóa và phân tích phần mềm', credit: 3, icon: 'folder_code'},
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

const graduationBlock = ref([
  {id: 25, code: 'TT6000', name: 'Thực tập tốt nghiệp thạc sĩ', credit: 6, icon: 'briefcase'},
  {id: 26, code: 'LV6002', name: 'Luận văn tốt nghiệp thạc sĩ', credit: 9, icon: 'scroll_text'},
])


const getRegistrationData = async () => {
  try {
    const res = await fetch(`${import.meta.env.BASE_URL}data.json`)
    hustRegistrationData.value = await res.json()
  } catch (e) {
    // Fallback data tĩnh nếu không có file data.json
  }
}

onMounted(getRegistrationData)
</script>

<style scoped>
.hust-dashboard {
  background-color: #f0f2f5;
  min-height: 100vh;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  color: #222;
  box-sizing: border-box;
}

*, *::before, *::after {
  box-sizing: inherit;
}

.hust-header {
  background-color: #7b0e11;
  color: #fff;
  padding: 12px 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 12px;
}

.header-title {
  margin: 0;
  font-size: 1.15rem;
  font-weight: 600;
  letter-spacing: 1px;
}

.header-right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.logo-en {
  width: 200px;
  height: 65px;
}

.dashboard-body {
  padding: 16px 20px;
}

.card {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
  border: 1px solid #e1e4e8;
  overflow: hidden;
}

.h-full {
  height: 100%;
}

.top-cards-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-bottom: 16px;
}

.stat-card {
  padding: 14px 16px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.table-card-compact {
  padding: 12px 0 0 0;
}

.px-10 {
  padding-left: 12px;
  padding-right: 12px;
}

.card-title {
  font-size: 0.8rem;
  font-weight: 700;
  color: #2c3e50;
  text-transform: uppercase;
}

.stat-main {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin: 8px 0;
}

.stat-number {
  font-size: 1.6rem;
  font-weight: 800;
  color: #000;
}

.stat-number.text-large {
  font-size: 2rem;
}

.stat-sub {
  font-size: 1.1rem;
  color: #444;
}

.font-bold {
  font-weight: 700;
}

.font-medium {
  font-weight: 500;
}

.progress-bar-container {
  width: 100%;
  height: 8px;
  background-color: #e5e7eb;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 6px;
}

.progress-bar-fill {
  height: 100%;
  background-color: #7b0e11;
  border-radius: 4px;
  transition: width 0.3s ease;
}

.input-group {
  margin: 6px 0 8px 0;
}

.custom-input {
  width: 100%;
  padding: 6px 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 0.75rem;
  outline: none;
}

.custom-input:focus {
  border-color: #7b0e11;
}

.btn-calculate {
  background-color: #7b0e11;
  color: #fff;
  border: none;
  padding: 8px;
  font-size: 0.75rem;
  font-weight: 700;
  border-radius: 4px;
  cursor: pointer;
  letter-spacing: 1px;
  width: 100%;
  transition: background-color 0.2s;
}

.btn-calculate:hover {
  background-color: #630a0d;
}

.main-columns-grid {
  display: grid;
  grid-template-columns: 1.1fr 1fr 1.3fr;
  gap: 16px;
  align-items: start;
}

.column-col {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.table-card {
  padding-bottom: 4px;
}

.table-header-title {
  font-size: 0.82rem;
  font-weight: 700;
  padding: 8px 12px;
  color: #111;
  letter-spacing: 0;
  text-transform: uppercase;
}

.pure-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.pure-table th {
  background-color: #e9ecef;
  color: #333;
  font-size: 0.72rem;
  font-weight: 600;
  padding: 6px 8px;
  border-bottom: 1px solid #d1d5db;
  white-space: nowrap;
}

.pure-table td {
  padding: 6px 8px;
  font-size: 0.75rem;
  border-bottom: 1px solid #f0f0f0;
  color: #222;
}

.pure-table tr:hover {
  background-color: #f8fafc;
}

.compact-table td,
.compact-table th {
  padding: 4px 10px;
}

.text-right {
  text-align: right;
}

.tabs-header {
  display: flex;
  border-bottom: 1px solid #e1e4e8;
  background-color: #f8f9fa;
}

.tab-btn {
  flex: 1;
  padding: 8px 10px;
  font-size: 0.75rem;
  font-weight: 600;
  border: none;
  background: transparent;
  cursor: pointer;
  color: #666;
  border-bottom: 2px solid transparent;
  transition: all 0.2s;
}

.tab-btn.active {
  color: #7b0e11;
  border-bottom: 2px solid #7b0e11;
  background: #fff;
}

@media (max-width: 1100px) {
  .top-cards-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .main-columns-grid {
    grid-template-columns: 1fr;
  }
}
</style>
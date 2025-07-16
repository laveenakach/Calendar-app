<template>
  <section
    class="relative flex flex-col items-start gap-6 p-4 w-full max-w-[1240px] bg-[#0F0F0F] text-white overflow-hidden"
  >
    <!-- Background gradient overlay -->
    <div
      class="absolute top-0 left-0 w-full h-[180px] opacity-30 pointer-events-none z-0"
      style="background: linear-gradient(180deg, #2E7FF1 0%, rgba(46, 127, 241, 0) 41.45%)"
    ></div>

    <!-- Top section (date & actions) -->
    <div class="relative z-10 w-full flex justify-between items-center px-12 py-6">
      <!-- Left controls -->
      <div class="flex items-center gap-4">
        <div class="flex w-[100px] h-[32px] px-[14px] py-[8px] justify-center items-center gap-[8px] rounded-full border border-[#2E7FF1]">
          <span>Today</span>
        </div>
        <div class="w-[32px] h-[32px] flex justify-center items-center bg-[#212226] rounded-full">
          <img src="/icons/chevron-left.svg" alt="chevron" class="w-4 h-4" />
        </div>
        <div class="w-[32px] h-[32px] flex justify-center items-center bg-[#212226] rounded-full">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="none" viewBox="0 0 16 16">
            <path fill-rule="evenodd" clip-rule="evenodd"
              d="M5.646 3.646a.5.5 0 0 1 .708 0l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L9.293 8 5.646 4.354a.5.5 0 0 1 0-.708Z"
              fill="#C6C8D2" />
          </svg>
        </div>
        <h1 class="text-lg font-semibold">13 January, 2025 - 19 January, 2025</h1>
        <div class="w-[32px] h-[32px] flex justify-center items-center bg-[#212226] rounded-full">
          <img src="/icons/right.svg" alt="right" class="w-4 h-4" />
        </div>
      </div>

      <!-- Right summary -->
      <div class="flex items-center gap-6">
        <div class="flex items-center h-[50px] px-6 py-3 gap-4 rounded-[12px] border border-[#2E7FF1] bg-[#0F0F0F] text-[#7F859F] text-base font-normal leading-6">
          <span>Grand Total</span>
          <div class="flex items-center gap-2 text-white text-lg font-bold leading-[26px]">
            ₹ 3,000
          </div>
        </div>
        <button class="bg-blue-500 text-white px-4 py-2 rounded">+ Add</button>
      </div>
    </div>

    <!-- Tabs and Filters Row -->
    <div class="w-full flex justify-between items-center mt-6">
      <!-- Tabs -->
      <div class="flex items-center gap-[21px] bg-[#2F323E] rounded-[8px] px-2 py-1">
        <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] text-white text-base font-normal leading-6">
          Daily
        </div>
        <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] bg-[#2E7FF1] text-white text-base font-normal leading-6">
          Weekly
        </div>
        <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] text-white text-base font-normal leading-6">
          Monthly
        </div>
        <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] text-white text-base font-normal leading-6">
          List
        </div>
      </div>

      <!-- Filters -->
      <div class="flex items-center gap-4">
        <div class="flex h-[48px] flex-col justify-center rounded-[8px] bg-[#2F323E]">
          <div class="flex px-4 py-2 items-center gap-2 text-white text-sm font-normal leading-[22px]">
            All Services
          </div>
        </div>
        <div class="flex h-[48px] flex-col justify-center rounded-[8px] bg-[#2F323E]">
          <div class="flex px-4 py-2 items-center gap-2 text-white text-sm font-normal leading-[22px]">
            All Tech
            <img src="/icons/right.svg" alt="right" class="w-4 h-4" />
          </div>
        </div>
      </div>
    </div>

    <!-- Weekly Grid with Vertical Lines and Day Labels -->
<div class="w-full mt-10 overflow-x-auto">
  <div class="grid grid-cols-7 gap-0 w-full">
    <div
      v-for="(day, index) in days"
      :key="index"
      class="flex flex-col items-center min-w-[90px] h-[600px] border-l border-[#2F323E] relative"
    >
      <!-- Day & Date Labels inside the column -->
      <div class="flex flex-col items-center pt-2 pb-3 z-10 bg-[#0F0F0F] w-full text-center">
        <span :class="['text-xs font-semibold', index > 4 ? 'text-gray-400' : 'text-white']">
          {{ day.day }}
        </span>
        <span :class="['text-xs font-semibold', index > 4 ? 'text-gray-400' : 'text-white']">
          {{ day.date }}
        </span>
      </div>

  
    </div>
  </div>
</div>


  </section>
</template>

<script setup>
const days = [
  { day: 'MON', date: '13' },
  { day: 'TUE', date: '14' },
  { day: 'WED', date: '15' },
  { day: 'THU', date: '16' },
  { day: 'FRI', date: '17' },
  { day: 'SAT', date: '18' },
  { day: 'SUN', date: '19' }
];
</script>

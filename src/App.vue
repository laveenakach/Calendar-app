<template>
  <div class="flex min-h-screen bg-[#0F0F0F] overflow-y-auto">
    <!-- Sidebar -->
    <aside class="flex flex-col w-[200px] h-full border-r border-[#212226] bg-black"></aside>

    <!-- Right side: header and main content -->
    <div class="flex flex-col flex-1 min-h-screen">
      <!-- Header -->
      <header class="flex items-center px-5 h-[60px] w-full border-b border-[#2F323E] bg-black text-white">
        <h1 class="text-lg font-semibold">Calendar</h1>
      </header>

      <!-- Main calendar section -->
      <section class="relative flex flex-col flex-1 items-start gap-6 px-4 pt-2 pb-1 w-full bg-[#0F0F0F] text-white overflow-hidden">
        <!-- Background gradient overlay -->
        <div
          class="absolute top-0 left-0 w-full h-[180px] opacity-30 pointer-events-none z-0"
          style="background: linear-gradient(180deg, #2E7FF1 0%, rgba(46, 127, 241, 0) 41.45%)"
        ></div>

        <!-- Top section (date & actions) -->
        <div class="relative z-10 w-full flex justify-between items-center px-12 py-2">
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
        <div class="w-full flex justify-between items-center mt-2">
          <!-- Tabs -->
          <div class="flex items-center gap-[21px] bg-[#2F323E] rounded-[8px] px-2 py-1">
            <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] text-white text-base font-normal leading-6">Daily</div>
            <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] bg-[#2E7FF1] text-white text-base font-normal leading-6">Weekly</div>
            <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] text-white text-base font-normal leading-6">Monthly</div>
            <div class="flex h-[48px] px-4 py-2 justify-center items-center gap-[10px] rounded-[8px] text-white text-base font-normal leading-6">List</div>
          </div>

          <!-- Filters -->
          <div class="flex items-center gap-4">
            <div class="flex h-[48px] flex-col justify-center rounded-[8px] bg-[#2F323E]">
              <div class="flex px-4 py-2 items-center gap-2 text-white text-sm font-normal leading-[22px]">All Services</div>
            </div>
            <div class="flex h-[48px] flex-col justify-center rounded-[8px] bg-[#2F323E]">
              <div class="flex px-4 py-2 items-center gap-2 text-white text-sm font-normal leading-[22px]">
                All Tech
                <img src="/icons/right.svg" alt="right" class="w-4 h-4" />
              </div>
            </div>
          </div>
        </div>

      <!-- Weekly Grid -->
      <div class="w-full flex-1 mt-3 overflow-x-auto relative">
  <div class="grid grid-cols-7 gap-0 min-h-full w-full max-h-[500px] overflow-y-auto pr-1">
    <div
      v-for="(day, index) in days"
      :key="index"
      class="flex flex-col items-center min-w-[90px] border-l border-[#2F323E] relative min-h-[500px]"
    >
      <!-- Header -->
      <div class="flex flex-col items-center pt-2 pb-3 z-10 bg-[#0F0F0F] w-full text-center">
        <span :class="['text-xs font-semibold', (day.day === 'SAT' || day.day === 'SUN') ? 'text-gray-500' : 'text-white']">
          {{ day.day }}
        </span>
        <span :class="['text-xs font-semibold', (day.day === 'SAT' || day.day === 'SUN') ? 'text-gray-500' : 'text-white']">
          {{ day.date }}
        </span>
      </div>

      <!-- Scheduled Cards -->
      <div class="flex flex-col items-start gap-2 px-2 w-full mt-2 z-10">
        <!-- === 13 Jan Cards === -->
        <template v-if="day.date === '13'">
          <!-- Top Row -->
          <div class="w-[280px] h-[30px] p-2 flex items-center gap-1 rounded-[8px] border border-[#2F323E] bg-[#B4DDF3]">
            <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
            <img src="/icons/image.svg" alt="img" class="w-4 h-4" />
            <div class="flex-1 text-ellipsis text-[#00285F] font-bold text-xs">Thomas Smith</div>
            <img src="/icons/calendar-blank.svg" alt="calendar" class="w-4 h-4" />
            <div class="text-xs font-semibold text-[#2F323E]">8:00 AM - 10:00 AM</div>
            <img src="/icons/timer.svg" alt="timer" class="w-4 h-4" />
          </div>

          <div class="w-[720px] h-[30px] p-2 flex items-center gap-1 rounded-[8px] border border-[#2F323E] bg-yellow-100">
            <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
            <img src="/icons/image.svg" alt="img" class="w-4 h-4" />
            <div class="text-[#00285F] font-bold text-xs whitespace-nowrap">Thomas Smith</div>
            <img src="/icons/calendar-blank.svg" alt="calendar" class="w-4 h-4" />
            <div class="text-xs font-semibold text-[#2F323E] whitespace-nowrap">8:00 AM - 10:00 AM</div>
            <img src="/icons/timer.svg" alt="timer" class="w-4 h-4" />
          </div>

          <div class="flex flex-col gap-[4px] mt-[80px]">
          <div class="mt-[2px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-[#CCC0E9] min-h-[100px] z-20">
            <div class="flex items-center gap-2">
              <img src="/icons/image.svg" class="w-4 h-4" />
              <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/user.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/package.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
            </div>
          </div>
          <div class="mt-[2px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-yellow-100 min-h-[100px] z-20">
            <div class="flex items-center gap-2">
              <img src="/icons/image.svg" class="w-4 h-4" />
              <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/user.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/package.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
            </div>
          </div>
          <div class="mt-[2px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-pink-100 min-h-[100px] z-20">
            <div class="flex items-center gap-2">
              <img src="/icons/image.svg" class="w-4 h-4" />
              <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/user.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
            </div>
            <div class="flex items-center gap-2">
              <img src="/icons/package.svg" class="w-4 h-4" />
              <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
            </div>
          </div>
          </div>
        </template>

        <!-- === 14 Jan Cards === -->
        <template v-if="day.date === '14'">
          <!-- Top Row -->
          <div class="mt-[80px] w-[430px] h-[30px] p-2 flex items-center gap-1 rounded-[8px] border border-[#2F323E] bg-purple-200">
            <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
            <img src="/icons/image.svg" alt="img" class="w-4 h-4" />
            <div class="text-[#00285F] font-bold text-xs whitespace-nowrap">Thomas Smith</div>
            <img src="/icons/calendar-blank.svg" alt="calendar" class="w-4 h-4" />
            <div class="text-xs font-semibold text-[#2F323E] whitespace-nowrap">8:00 AM - 10:00 AM</div>
          </div>

          <div class="w-[430px] h-[30px] p-2 flex items-center gap-1 rounded-[8px] border border-[#2F323E] bg-green-200">
            <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
            <img src="/icons/image.svg" alt="img" class="w-4 h-4" />
            <div class="text-[#00285F] font-bold text-xs whitespace-nowrap">Thomas Smith</div>
            <img src="/icons/calendar-blank.svg" alt="calendar" class="w-4 h-4" />
            <div class="text-xs font-semibold text-[#2F323E] whitespace-nowrap">8:00 AM - 10:00 AM</div>
          </div>

          <!-- Bottom Cards -->
          <div class="flex flex-col gap-[4px] mt-[1px]">
            <div class="mt-[1px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-orange-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[1px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-red-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[1px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-blue-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
          </div>
        </template>

        <!-- === 15 Jan Cards === -->
        <template v-if="day.date === '15'">
          <div class="flex flex-col gap-[4px] mt-[105px]">
            <div class="mt-[50px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-orange-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[2px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-red-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[2px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-blue-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
          </div>
        </template>

        <!-- === 16 Jan Cards === -->
        <template v-if="day.date === '16'">
          <div class="flex flex-col gap-[4px] mt-[1px]">
             <div class="mt-[155px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-green-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[2px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-blue-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
          </div>
        </template>

        <!-- === 17 Jan Cards === -->
        <template v-if="day.date === '17'">
          <div class="flex flex-col gap-[4px] mt-[1px]">
            <div class="mt-[158px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-orange-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[1px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-red-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
            <div class="mt-[1px] w-[150px] p-3 flex flex-col gap-2 rounded-[8px] border border-[#2F323E] bg-blue-200 min-h-[100px] z-20">
              <div class="flex items-center gap-2">
                <img src="/icons/image.svg" class="w-4 h-4" />
                <div class="text-xs font-semibold text-[#00285F]">Client Name</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/calendar-blank.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">8:00 AM - 10:00 AM</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/user.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Arlene McCoy</div>
              </div>
              <div class="flex items-center gap-2">
                <img src="/icons/package.svg" class="w-4 h-4" />
                <div class="text-xs text-[#2F323E]">Package name, ... +2</div>
              </div>
            </div>
          </div>
        </template>
      </div>
    </div>
  </div>
</div>

      </section>
    </div>
  </div>
</template>

<script setup>
import CardClient from './components/CardClient.vue'
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

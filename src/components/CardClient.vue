<template>
  <div>
    <!-- Top Row -->
    <div class="flex items-center gap-2">
      <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
      <img src="/icons/image.svg" alt="img" class="w-4 h-4" />
      <div class="text-[#00285F] text-xs font-bold truncate">{{ title }}</div>
    </div>

    <!-- Time -->
    <div class="flex items-center gap-2">
    <img src="/icons/calendar-blank.svg" alt="calendar" class="w-4 h-4" />
      <div class="text-xs font-semibold text-[#2F323E]">{{ time }}</div>
    </div>

    <!-- Person -->
    <div class="flex items-center gap-2">
      <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
      <img src="/icons/user.svg" alt="user" class="w-4 h-4" />
      <div class="text-[#00285F] text-xs font-bold truncate">{{ person }}</div>
    </div>

    <!-- Package -->
    <div class="flex items-center gap-2">
      <div class="w-4 h-4 rounded-full bg-cover bg-center" style="background-image: url('/path-to-image.jpg')"></div>
      <img src="/icons/package.svg" alt="pkg" class="w-4 h-4" />
      <div class="text-[#00285F] text-xs font-bold truncate">{{ package }}</div>
    </div>
  </div>
</template>

<script setup>
defineProps(['title', 'time', 'person', 'package'])
</script>

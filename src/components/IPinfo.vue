<template>
    <div class="absolute -bottom-64 lg:-bottom-20 flex flex-col lg:flex-row bg-white gap-y-4 gap-x-12 px-8 pt-8 pb-12 rounded-md">
        <div class="flex flex-col">
            <h3 class="text-xs mb-2 uppercase">ip address</h3>
            <span class="text-2xl">{{ipInfo.address}}</span>
        </div>
        <div class="flex flex-col">
            <h3 class="text-xs mb-2 uppercase">Location</h3>
            <span class="text-2xl">{{ipInfo.state}}</span>
        </div>
        <div class="flex flex-col">
            <h3 class="text-xs mb-2 uppercase">TimeZone</h3>
            <span class="text-2xl">{{ipInfo.timezone}}</span>
        </div>
        <div class="flex flex-col">
            <h3 class="text-xs mb-2 uppercase">Isp</h3>
            <span class="text-2xl">{{ipInfo.isp}}</span>
        </div>
    </div>
</template>
<script setup>
import { defineProps } from 'vue'
defineProps({
  ipInfo: {
    type: Object,
    required: false,
  },
});
</script>
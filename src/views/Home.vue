<template>
    <div class="flex flex-col h-screen max-h-screen">
        <!-- search -->
        <div class="flex justify-center relative px-4 pt-8 pb-32 bg-teal-600">
            <!-- search input -->
            <div class="w-full max-w-screen-sm">
                <h1 class="text-white text-center text-3xl pb-4"> ip address tracker</h1>
                <div class="flex">
                    <input class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none" type="text" placeholder="insert your ip address here">
                    <i class="flex cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md fas fa-chevron-right items-center"></i>
                </div>
            </div>
            <!-- IPinfo -->
            <IPinfo />
        </div>
    </div>
</template>

<script setup>
import { defineComponent } from 'vue';
import IPinfo from '../components/IPinfo.vue'

const __name = "Home";

</script>
<template>
    <div class="flex flex-col h-screen max-h-screen">
        <!-- search -->
        <div class="z-20 flex justify-center relative px-4 pt-8 pb-32 bg-teal-600">
            <!-- search input -->
            <div class="w-full max-w-screen-sm">
                <h1 class="text-white text-center text-3xl pb-4"> ip address tracker</h1>
                <div class="flex">
                    <input v-model="queryIp" class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none" type="text" placeholder="insert your ip address here">
                    <i @click="getIpINfo" class="flex cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md fas fa-chevron-right items-center"></i>
                </div>
            </div>
            <!-- IPinfo -->
            <IPinfo v-if="ipInfo" :ipInfo="ipInfo" />
        </div>
        <!-- map -->
        <div id="mapid" class="h-full z-10"></div>
    </div>
</template>

<script setup>
import { defineComponent, onMounted, ref } from 'vue';
import IPinfo from '../components/IPinfo.vue'
import leaflet from 'leaflet'
import axios from 'axios'

const __name = "Home";

let mymap;

const queryIp = ref("")
const ipInfo = ref(null)

onMounted(() => {
    mymap = leaflet.map('mapid').setView([ 55.67, 12.56], 13);

    leaflet.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    accessToken: import.meta.env.VITE_MAPBOX_KEY,
    attribution: '&copy; <a href="http://www.mapbox.com/copyright">mapbox</a>'
}).addTo(mymap);
});
const getIpINfo = async() => {
    try {
        const data = await axios.get(`https://geo.ipify.org/api/v2/country,city?apiKey=${import.meta.env.VITE_IP_GEO_KEY}&ipAddress=${queryIp.value}`)
        const result = data.data
            console.log(result)
        ipInfo.value = {
            address: result.ip,
            state: result.location.region,
            timezone: result.location.timezone,
            isp: result.isp,
            lat: result.location.lat,
            lng: result.location.lng
        }
        leaflet.marker([ipInfo.value.lat, ipInfo.value.lng]).addTo(mymap);
        mymap.setView([ipInfo.value.lat, ipInfo.value.lng], 13);
    } catch (error) {
        alert(error.message)
    }
}

</script>
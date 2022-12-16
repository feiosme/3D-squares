<!--
 * @Author: feiosme
 * @LastEditors: feiosme
 * @Description:
-->
<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import './assets/styles/color.css';
import Squares from './squares/Squares.vue';
import Footer from '@/components/footer/Footer.vue'
</script>

<template>
    <div class="flex items-center justify-center w-full h-[90vh] sm:h-screen transition-all relative">
        <Squares />
    </div>
    <!-- <Footer /> -->
</template>

<style lang="scss">
div {
    @apply font-bold;
    font-family: "DIN-Condensed";
    font-size: 30px;
}

body {
    @apply bg-gray-700;
}
</style>

<!--
 * @Author: feiosme
 * @LastEditors: feiosme
 * @Description: 
 * @FilePath: /3D-squares/src/components/footer/Footer.vue
-->
<template>
    <div
        class="absolute bottom-1 inset-x-0 flex flex-col items-center justify-end transform origin-center scale-50 sm:scale-75 xl:scale-90 text-gray-600 select-none pointer-events-none">
        <div>
            &copy; ZHANG ZY
        </div>
        <!-- <div class="absolute transform translate-y-8">
            <transition appear enter-active-class="transition transform ease-zoomInLeft"
                enter-from-class="transform opacity-0" enter-to-class="transform opacity-100"
                leave-active-class="transition-all transform origin-center ease-zoomOutRight"
                leave-from-class="transform opacity-100" leave-to-class="transform opacity-0">
                <div v-if="!open" class="w-36 h-1 bg-gray-600 overflow-hidden">
                    <transition appear enter-active-class="transition transform ease-zoomInLeft duration-[5000ms]"
                        enter-from-class="transform -translate-x-full" enter-to-class="transform translate-x-0">
                        <div class="h-1 w-full bg-gray-400" />
                    </transition>
                </div>
            </transition>
        </div> -->
    </div>
</template>

<script>
export default {
    name: "Footer",
    props: {
        open: {
            type: Boolean,
            default: false
        }
    },
    setup() {
        return {

        }
    }
}
</script>
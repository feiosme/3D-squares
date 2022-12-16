<!--
 * @Author: feiosme
 * @LastEditors: feiosme
 * @Description:
-->
<!-- npx tailwindcss -i ./src/assets/style.css -o ./dist/style.css --watch -->
<template>
    <div class="w-[372px] h-[372px] overflow-hidden transform -translate-x-1.5 -translate-y-1.5">
        <div class="ml-3 mt-3 w-[360px] h-[360px] grid grid-cols-9 transition" :class="open ? 'bg-black' : ''">
            <div v-for="(item, i) in squares" :key="item" class="w-[40px] h-[40px] text-center relative transition z-10"
                :class="[open ? 'bg-black-' : '', exception.includes(i) ? '' : 'select-none pointer-events-none']">
                <transition appear enter-active-class="transition transform ease-zoomInLeft duration-700"
                    :style="'transition-delay:' + (item.delay + 1) * 50 + 'ms'" enter-from-class="transform opacity-0"
                    enter-to-class="transform opacity-100"
                    leave-active-class="transition-all transform origin-center ease-zoomOutRight"
                    leave-from-class="transform opacity-100" leave-to-class="transform opacity-0">
                    <div v-if="show" class="absolute bottom-0 right-0">
                        <div :id="i"
                            class="absolute bottom-0 right-0 w-[40px] h-[40px] transition-all transform border border-black"
                            :style="[`transition-delay: ${(item.delay + 1) * 50}ms`, `transition-duration: ${(item.high + 1) * 50 + 300}ms`, `transform: translateX(${item.high * 0.03 * -1}rem) translateY(${item.high * 0.03 * -1}rem)`]">
                            <!-- :style="['transition-delay: ' + item.high*100 + 'ms', 'transform: translate( -'+ item.high*0.05 +'rem, -'+ item.high*0.05 +'rem);']" -->
                            <div class="absolute transition-color z-20 inset-0"
                                :class="item.color == color[0] ? 'text-gray-100' : 'text-gray-900'"
                                :style="'transition-delay:' + (item.delay + 1) * 50 + 'ms'">
                                <!-- <span v-if="i == 38">Z</span> -->
                                <span v-if="i == 39">Z</span>
                                <span v-if="i == 40">Z</span>
                                <span v-if="i == 41">Y</span>
                                <!-- <span v-if="i == 42">G</span> -->
                                <a v-if="i == 49" href="https://www.feios.me"
                                    class="w-full h-full flex items-center justify-center transition cursor-pointer opacity-30 hover:opacity-80"
                                    @mouseover="setTips('博客')" @mouseleave="setTips(null)">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20"
                                        fill="currentColor">
                                        <path
                                            d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z" />
                                    </svg>
                                </a>
                                <span v-if="i == 76"
                                    class="w-full h-full flex items-center justify-center transition cursor-pointer opacity-30 hover:opacity-80"
                                    @click="reset" @mouseover="setTips('刷新方块')" @mouseleave="setTips(null)">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20"
                                        fill="currentColor">
                                        <path fill-rule="evenodd"
                                            d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z"
                                            clip-rule="evenodd" />
                                    </svg>
                                </span>
                                <a v-if="i == 58" href="https://github.com/feiosme/3D-squares"
                                    class="w-full h-full flex items-center justify-center transition cursor-pointer opacity-30 hover:opacity-80"
                                    @mouseover="setTips('Github 项目')" @mouseleave="setTips(null)">
                                    <img src="@/assets/icons/github.svg" class="p-2.5" />
                                </a>
                            </div>
                            <div class="absolute w-full h-full transition-all z-10"
                                :style="['transition-delay:' + (item.delay + 1) * 50 + 'ms', 'background-color: ' + item.color]" />
                            <div class="absolute top-0 left-0 transform origin-bottom-right -translate-y-[12.7px] translate-x-[10.75px] -rotate-45 h-10 bg-black"
                                style="width: 56.5685425px;" />
                        </div>
                    </div>
                </transition>
            </div>
        </div>
    </div>

    <div
        class="absolute bottom-1 inset-x-0 flex flex-col items-center justify-end transform origin-center scale-50 sm:scale-75 xl:scale-90 select-none pointer-events-none">
        <span class="sm:hidden text-gray-600">
            主页
        </span>
        <span class="hidden sm:block text-gray-200">
            {{ tips }}
        </span>
    </div>

    <!-- <div
        class="fixed bottom-0 inset-x-0 inline-flex items-center"
    >
        <button class="px-2 text-white mx-auto rounded-md" @click="reset">
            reset
        </button>
    </div> -->

    <!-- <div class="bg-1 bg-2 bg-3 bg-4 bg-0 -translate-y-1"></div> -->
</template>

<script>
import { ref, onMounted } from 'vue';
import faker from '@faker-js/faker/locale/zh_CN';
import velocity from 'velocity-animate';
export default {
    name: 'Bg',
    setup() {
        const open = ref(true);
        const squares = ref([]);
        const show = ref(true);
        const color = {
            0: '#4E64A6',
            1: '#49BF51',
            2: '#F2CB05',
            3: '#F28322',
            4: '#F25050'
        };

        const exception = [
            49,
            76,
            58
        ]

        function Timer(fn, t) {
            let timer = window.setInterval(fn, t);

            this.stop = () => {
                if (timer) {
                    window.clearInterval(timer);
                    timer = null;
                }
                return this;
            };

            this.start = () => {
                if (!timer) {
                    this.stop();
                    timer = window.setInterval(fn, t);
                }
                return this;
            };

            this.reset = (newT) => {
                t = newT;
                this.stop();
                this.start();
                return this;
            };
        }

        // const timeDelay = new Timer(() => {
        //     for(let i = 0; i < 81; i++) {
        //         const ele = document.getElementById(i);
        //         console.log(ele);
        //         const num = faker.datatype.number(9) * 0.05 * -1;
        //         velocity(ele,{
        //             translateX: num+'rem',
        //             translateY: num+'rem'
        //         });
        //     }
        // },5000);

        const setSquares = () => {
            squares.value = [];
            for (let i = 0; i < 81; i++) {
                squares.value.push({
                    color: color[faker.datatype.number(4)],
                    delay: faker.datatype.number(18),
                    high: 0
                });
            }
            setTimeout(() => {
                for (let i = 0; i < 81; i++) {
                    squares.value[i].high = faker.datatype.number(18);
                }
                console.log(squares.value);
            }, 700);
        };

        const timeDelay = new Timer(() => {
            // open.value = true;
            // show.value = true;
            setTimeout(() => {
                for (let i = 0; i < 81; i++) {
                    // const ele = document.getElementById(i);
                    // console.log(ele);
                    squares.value[i].color = color[faker.datatype.number(4)];
                    squares.value[i].high = faker.datatype.number(18);
                    // const num = squares.value[i].high * 0.03 * -1;
                    // velocity(ele,{
                    //     translateX: 0,
                    //     translateY: 0
                    // });
                    // velocity(ele,{
                    //     translateX: num+'rem',
                    //     translateY: num+'rem'
                    // });
                }
            }, 700);

        }, 5000);

        onMounted(() => {
            setSquares();
        });

        const toggle = () => {
            if (open.value) {
                timeDelay.stop();
                for (let i = 0; i < 81; i++) {
                    // const ele = document.getElementById(i);
                    // squares.value[i].color = '';
                    squares.value[i].high = 0;
                    // velocity(ele,{
                    //     translateX: 0,
                    //     translateY: 0
                    // });
                }
                // max 18*50+300 = 1200ms
                setTimeout(() => {
                    show.value = false;
                }, 1200);
            } else {
                timeDelay.reset(5000);
                show.value = true;
            }
            open.value = !open.value;
        };

        const reset = () => {
            timeDelay.reset(5000);
            for (let i = 0; i < 81; i++) {
                // const ele = document.getElementById(i);
                // squares.value[i].color = '';
                squares.value[i].high = 0;
                // velocity(ele,{
                //     translateX: 0,
                //     translateY: 0
                // });
            }
            // max 18*50+300 = 1200ms
            setTimeout(() => {
                show.value = false;
            }, 1200);
            // max 18*50 = 900ms
            setTimeout(() => {
                setSquares();
                show.value = true;
            }, 2200);
        };

        const mouseover = (i) => {
            const ele = document.getElementById(i);
            velocity(ele, {
                translateX: 0,
                translateY: 0
            });
        };

        // hover tips
        const tips = ref(null)
        const setTips = (t) => {
            tips.value = t
        }

        return {
            open,
            color,
            exception,
            squares,
            show,
            tips,
            toggle,
            reset,
            mouseover,
            setTips
        };
    }
};
</script>

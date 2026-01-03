<script setup>
import { Circle, Heart, Award } from 'lucide-vue-next';
import { ref } from 'vue';

const fill = ref();

const addFill = () => {
    fill.value.classList.add('animate-fill')
    setTimeout(() => {
        fill.value.classList.remove('animate-fill')
    }, 1500)
}

</script>
<template>
    <section
        class="relative overflow-hidden bg-gray-50 dark:bg-[#18181a] py-12 px-6 sm:px-8 md:px-10 lg:py-24 lg:px-24 flex flex-col lg:flex-row items-center justify-between transition-all duration-200 ease-in-out">
        <div
            class="w-44 h-44 bg-blue-600 blur-[125px] absolute left-1/2 top-1/2 transform -translate-x-1/2 -translate-y-[60%] rounded-full">
        </div>
        <div class="flex-1 lg:ml-28 w-full max-w-xl space-y-6 relative z-20 ">
            <h2 class="text-4xl sm:text-5xl text-gray-900 dark:text-slate-50 text-center lg:text-left mt-8 lg:mt-0 transition-all duration-300 ease-in-out "
                data-aos="fade-right">
                <div class="group relative inline-block py-2.5 px-2" @mouseenter="addFill">
                    Profesionals
                    <span class="absolute inset-0 -z-10 bg-blue-600 border-l-4 w-0" ref="fill"></span>
                </div>
                <span
                    class="mt-2 font-bold text-black dark:text-white block lg:inline transition-all duration-300 ease-in-out">Service</span>
                <span class="text-green-500">.</span>
            </h2>
            <div class="flex gap-3 mt-4 justify-center lg:justify-start" data-aos="fade-right" data-aos-delay="100">
                <Circle class="text-pink-500 w-5 h-5" />
                <Circle class="text-yellow-500 w-5 h-5" />
                <Circle class="text-green-500 w-5 h-5" />
            </div>
            <div class="flex flex-col lg:grid lg:grid-cols-2 gap-6 lg:gap-48 items-center lg:items-start">
                <div class="bg-white dark:bg-[#272729] w-72 rounded-3xl p-6 border border-gray-100 dark:border-[#505050] shadow-xl lg:shadow-2xl transition-all duration-300 ease-in-out"
                    data-aos="zoom-in" data-aos-delay="200">
                    <div class="ml-4 w-10 h-10 flex items-center justify-center rounded-lg bg-pink-100 mb-4">
                        <span class="text-pink-500 text-xl">
                            <Heart class="text-pink-600 w-6 h-6" />
                        </span>
                    </div>
                    <h3
                        class="ml-4 text-lg font-semibold text-gray-600 dark:text-white transition-all duration-300 ease-in-out">
                        Service Subtitle One</h3>
                    <p class="ml-4 text-slate-500 dark:text-slate-200 text-sm transition-all duration-300 ease-in-out">
                        Lorem ipsum dolor sit amet consectetur
                        adipisicing.</p>
                </div>
                <div class="bg-white dark:bg-[#272729] w-72 rounded-3xl p-6 border border-gray-100 dark:border-[#505050] shadow-xl lg:shadow-2xl transition relative z-30"
                    data-aos="zoom-in" data-aos-delay="300">
                    <div class="ml-4 w-10 h-10 flex items-center justify-center rounded-lg bg-yellow-100 mb-4">
                        <Award class="text-yellow-600 w-6 h-6" />
                    </div>
                    <h3 class="ml-4 text-lg font-semibold text-gray-600 dark:text-white">Service Subtitle One</h3>
                    <p class="ml-4 text-slate-500 dark:text-slate-200 text-sm">Lorem ipsum dolor sit amet consectetur
                        adipisicing.</p>
                </div>
            </div>
        </div>
        <div class="flex mt-12 lg:mt-0 lg:ml-12 relative w-full justify-center" data-aos="fade-left"
            data-aos-delay="400">
            <div
                class="w-64 h-64 sm:w-80 sm:h-80 md:w-96 md:h-96 lg:w-[600px] lg:h-[500px] overflow-hidden border-8 border-white dark:border-[#505050] shadow-lg lg:shadow-lg rounded-[60%_40%_30%_60%/60%_30%_70%_30%] relative z-10">
                <img src="/img/hero/hero.webp" class="w-full h-full object-cover" alt="">
            </div>
        </div>
    </section>
</template>
<style scoped></style>
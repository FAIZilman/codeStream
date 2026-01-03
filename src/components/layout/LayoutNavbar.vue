<script setup>
import { onMounted, ref, useTemplateRef } from 'vue';
import { X, Menu, Sun, MoonStar } from 'lucide-vue-next';
// import SectionAbout from '../sections/SectionAbout.vue';

const isMenuOpen = ref(false);
const toggleMenu = () => {
    isMenuOpen.value = !isMenuOpen.value
}

const { darkMode } = defineProps({
    'darkMode': {
        type: Boolean,
    }
});

const menuItems = [
    {
        name: "Home",
        path: "#"
    },
    {
        name: "About",
        path: "#about"
    },
    {
        name: "Company",
        path: "#company"
    },
    {
        name: "Services",
        path: "#services"
    },
    // {
    //     name: "Contact",
    //     path: "#contact"
    // },
]

let location = ref(window.location.hash);


const navbarRef = useTemplateRef('navbar');
onMounted(() => {
    window.addEventListener('hashchange', () => {
        location.value = window.location.hash == '' ? '#' : window.location.hash
    })
    function showSticky() {
        navbarRef.value.classList.add("bg-white")
        navbarRef.value.classList.add("dark:bg-[#272729]")
        navbarRef.value.classList.add("sticky")
    }

    function hideSticky() {
        navbarRef.value.classList.remove("bg-white")
        navbarRef.value.classList.remove("dark:bg-[#272729]")
        navbarRef.value.classList.remove("sticky")
    }

    document.addEventListener('scroll', () => {
        if (window.scrollY >= navbarRef.value.clientHeight + 40) {
            showSticky()
        } else {
            hideSticky()
        }

        // window.
        // navbarRef.value.clientHeight
        // console.log(window.innerHeight)
        // console.log(navbarRef.value.clientHeight)
        // console.log()
        // if (!l.isIntersecting) {
        // l.target.classList.add('sticky')
        // } else {
        // l.target.classList.remove('sticky')
        // }
    });

    // observer.observe(navbarRef.value)
});

// window.addEventListener('scroll', (e) => {
// });

</script>

<template>
    <nav class="w-full top-0 left-0 right-0 z-50 bg-gray-50 dark:bg-[#18181a] transition-all ease-in-out shadow-2xl"
        ref="navbar">
        <div class="transition-all animation-sticky" ref="animation-sticky">
            <div
                class="max-w-7xl mx-auto px-4 sm:px-6 md:px-12 lg:px-20 py-3 md:py-4 flex items-center justify-between ">

                <!-- LOGO -->
                <div class=" flex items-start px-6 rounded-md">

                    <!-- Small Logo -->
                    <div
                        class="flex items-center gap-1 dark:text-white text-black text-xl font-semibold tracking-tight">
                        <span class="text-blue-500 text-4xl mb-2">
                            c
                        </span>
                        <span class="relative inline-block">
                            o
                            <!-- small liquid accent -->
                            <span class="absolute -top-0.5 left-1/2 -translate-x-1/2
               w-3 h-1 dark:bg-white bg-black  rounded-full">
                            </span>
                        </span>
                        de
                        <span class="relative inline-block">
                            St
                            <span class="absolute -top-0.5 left-1/2
               w-2.5 h-1 dark:bg-white bg-black rounded-full">
                            </span>
                        </span>
                        ream
                    </div>

                </div>

                <!-- LINKS! -->

                <ul class="hidden md:flex items-center gap-6 lg:gap-8 text-gray-700 dark:text-slate-50 font-medium">
                    <li v-for="({ name, path }, key) in menuItems" :key="name + key"
                        class="hover:text-green-500 cursor-pointer transition-colors"
                        :class="location == path ? 'text-green-500' : ''">
                        <a :href="path">{{ name }}</a>
                    </li>
                </ul>


                <!-- Button -->
                <div class="hidden md:flex md:items-center gap-x-5">
                    <!-- Toggling Dark Mode -->
                    <div @click="$emit('darkEvent')"
                        class="w-[64px] border border-slate-300 dark:border-[#404042] h-full rounded-full inset-shadow-sm shadow-xs bg-slate-50 dark:bg-[#28282a] relative flex transition-all ease-in-out duration-200 px-1.5 py-1 hover:border-blue-300  cursor-pointer">
                        <!-- <input type="checkbox" v-model="darkMode"
                        class=" top-0 bottom-0 left-0 right-0 absolute cursor-pointer bg-red-500"> -->
                        <div class="w-fit h-fit p-1.5 rounded-full shadow-md bg-white dark:bg-[#505050] cursor-pointer transition-all"
                            :class="darkMode ? 'translate-x-5' : ''">
                            <MoonStar v-if="darkMode" class="" size="16" color="white" stroke-width="2"></MoonStar>
                            <Sun v-else class="" size="16" color="oklch(68.1% 0.162 75.834) " stroke-width="2"></Sun>
                        </div>
                    </div>
                    <button
                        class="px-4 py-2 sm:px-5 sm:py-2 rounded-lg bg-blue-500 text-white font-medium hover:bg-blue-600 transition-colors">
                        Get Started
                    </button>
                </div>

                <!-- Mobile Menu -->
                <div class="flex gap-x-2 md:hidden">
                    <div @click="$emit('darkEvent')"
                        class="w-[64px] border border-slate-300 dark:border-[#404042] h-full rounded-full inset-shadow-sm shadow-xs bg-slate-50 dark:bg-[#28282a] relative flex transition-all ease-in-out duration-200 px-1.5 py-1 hover:border-blue-300  cursor-pointer">
                        <!-- <input type="checkbox" v-model="darkMode"
                        class=" top-0 bottom-0 left-0 right-0 absolute cursor-pointer bg-red-500"> -->
                        <div class="w-fit h-fit p-1.5 rounded-full shadow-md bg-white dark:bg-[#505050] cursor-pointer transition-all"
                            :class="darkMode ? 'translate-x-5' : ''">
                            <MoonStar v-if="darkMode" class="" size="16" color="white" stroke-width="2"></MoonStar>
                            <Sun v-else class="" size="16" color="oklch(68.1% 0.162 75.834) " stroke-width="2"></Sun>
                        </div>
                    </div>

                    <button @click="toggleMenu"
                        class="p-1 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <component :is="isMenuOpen ? X : Menu" class="w-6 h-6 text-gray-700 dark:text-white" />
                    </button>
                </div>

            </div>
            <!-- Mobile Menu -->
            <Transition>
                <div v-if="isMenuOpen"
                    class="md:hidden bg-white dark:bg-[#18181a] shadow-lg border-t border-gray-200 dark:text-white">
                    <div class="px-4 py-3 space-y-3 text-gray-700 dark:text-white">
                        <a v-for="({ name, path }, key) in menuItems" :key="name + key" :href="path"
                            class="block py-2 px-4  hover:bg-gray-100  dark:hover:bg-[#3a3a3a] rounded-lg hover:text-green-500"
                            :class="location == path ? 'dark:text-green-500 text-green-500' : ''">
                            {{ name }}</a>
                        <div class="pt-2">
                            <button
                                class="w-full py-2 rounded-lg bg-blue-500 text-white font-medium hover:bg-blue-600 transition-colors">Get
                                Started</button>
                        </div>
                    </div>
                </div>
            </Transition>
        </div>
    </nav>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
    transition: transform 0.2s ease;
}

.v-enter-from,
.v-leave-to {
    transform: translateY(-50%);
}
</style>
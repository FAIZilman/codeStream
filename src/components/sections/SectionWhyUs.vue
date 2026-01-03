<script setup>
import { Circle, Shield, Star, Zap } from 'lucide-vue-next';
import { onMounted, reactive, useTemplateRef } from 'vue';

const features = [
    {
        icon: Star,
        iconColor: 'text-blue-600',
        title: 'Excellence Guaranteed',
        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Eveniet, eius!',
        aos: 'fade-right',
        delay: '200'
    },
    {
        icon: Shield,
        iconColor: 'text-purple-600',
        title: 'Trust & Realiability',
        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Eveniet, eius!',
        aos: 'fade-right',
        delay: '300'
    },
    {
        icon: Zap,
        iconColor: 'text-pink-600',
        title: 'Innovation Driven',
        description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Eveniet, eius!',
        aos: 'fade-right',
        delay: '400'
    },
];


const statisctics = reactive([
    {
        value: '500',
        simbol: '+',
        label: 'Projects Completed',
        aos: 'fade-up',
        delay: '300'
    },
    {
        value: '10',
        simbol: '+',
        label: 'Years Experience',
        aos: 'fade-up',
        delay: '400'
    },
    {
        value: '99',
        simbol: '%',
        label: 'Success Rate',
        aos: 'fade-up',
        delay: '500'
    },
]);

const counting = useTemplateRef('counting');
// console.log(counting)

onMounted(() => {

    function hitung(value, maksimal, element) {
        let hitung = setInterval(() => {
            if (value >= maksimal) {
                clearInterval(hitung)
            }
            element.innerText = value++
        }, 30)
    }
    function handler(targets) {
        for (const [index, target] of Object.entries(targets)) {
            if (target.isIntersecting) {
                hitung(0, statisctics[index].value, target.target)
                observer.unobserve(target.target);
            }
        }
    }

    let observer = new IntersectionObserver(handler, {
        threshold: 0,
        rootMargin: '0px',
        once: true,
    })

    counting.value.forEach(element => {
        observer.observe(element)
    });
})

</script>
<template>
    <section id="company"
        class="relative overflow-hidden bg-gradient-to-br from-blue-50 to-purple-50 dark:from-[#151516] dark:to-[#3d3d3f] py-12 px-4 sm:py-16 md:py-20 md:px-12 lg:px-20">
        <div class="max-w-6xl mx-auto ">
            <div class="text-center mb-6 md:mb-8" data-aos="fade-down">
                <h2 class="text-4xl sm:text-5xl text-gray-900 dark:text-slate-100">
                    Agency
                    <span class="font-bold text-black dark:text-blue-500">Company ?</span>
                </h2>
                <div class="flex gap-3 mt-4 justify-center" data-aos="fade-right" data-aos-delay="100">
                    <Circle class="text-pink-500 w-5 h-5" />
                    <Circle class="text-yellow-500 w-5 h-5" />
                    <Circle class="text-green-500 w-5 h-5" />
                </div>
            </div>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 md:gap-12 items-center">
                <div class="relative w-full flex justify-center order-2 lg:order-1">
                    <div class="w-full max-w-md lg:max-w-lg xl:max-w-xl h-[460px] sm:h-[500px] md:h-[500px] lg:h-[600px] overflow-hidden bg-gray-50 shadow-lg md:shadow-xl rounded-[30%_10%_20%_70%/60%_30%_70%_30%] absolute top-0 z-0 dark:bg-[#303032]"
                        data-aos="fade-right" data-aos-delay="100">
                    </div>
                    <div class="space-y-4 sm:space-y-6 md:space-y-8 relative z-10 p-4 sm:p-6 w-full max-w-md ">
                        <div v-for="(feature, index) in features" :key="index"
                            class="flex items-start gap-2 p-4 sm:p-6 transi tion-all bg-transparent"
                            :data-aos="feature.aos" :data-aos-delay="feature.delay">
                            <div class="flex-shrink-0 w-10 h-10 sm:w-12 sm:h-12 flex items-center justify-center ">
                                <component :is="feature.icon"
                                    :class="`w-5 h-5 sm:w-6 sm:h-6 md:w-7 md:h-7 ${feature.iconColor}`" />
                            </div>
                            <div>
                                <h3 class="text-lg sm:text-xl font-semibold text-gray-900 dark:text-white mb-2">{{
                                    feature.title }}</h3>
                                <p class="text-gray-600 dark:text-slate-200 text-sm sm:text-base">{{ feature.description
                                    }}</p>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- Right Side - Statisctic -->
                <div class="relative order-1 lg:order-2">
                    <div class="bg-gradient-to-br from-yellow-600 to-pink-600 rounded-2xl md:rounded-3xl p-6 md:p-8 text-white h-80 sm:h-96 flex flex-col justify-center"
                        data-aos="zoom-in" data-aos-delay="200">
                        <div class="max-w-md mx-auto text-center">
                            <div
                                class="w-16 h-16 sm:w-20 sm:h-20 rounded-full bg-white/20 flex items-center justify-center mx-auto mb-4 sm:mb-6">
                                <Star class="w-8 h-8 sm:w-10 sm:h-10" />
                            </div>
                            <h3 class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4">
                                98% Customer Satisfaction
                            </h3>
                            <p class="mb-4 sm:mb-6 text-sm sm:text-base">
                                Our Client consistemly rate us as exceptional in quality and service delivery.
                            </p>
                            <div class="flex justify-center gap-3 sm:gap-4">
                                <div v-for="(statisctic, index) in statisctics" :key="index" class="text-center"
                                    :data-aos="statisctic.aos" :data-aos-delay="statisctic.delay">
                                    <div class="text-2xl sm:text-3xl font-bold"> <span ref="counting"></span>{{
                                        statisctic.simbol
                                    }} </div>
                                    <div class="text-xs sm:text-sm">{{ statisctic.label }} </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="absolute -top-8 -right-6 border-4 w-20 h-20 sm:w-24 sm:h-24 md:w-28 md:h-28 rounded-full border-yellow-500 opacity-50 hidden md:block"
                        data-aos="zoom-in" data-aos-delay="600">
                    </div>
                    <div class="absolute -bottom-8 -left-14 border-4 w-16 h-16 sm:w-20 sm:h-20 md:w-24 md:h-24 rounded-full border-pink-500 opacity-50 hidden md:block"
                        data-aos="zoom-in" data-aos-delay="700">
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>


<style scoped></style>
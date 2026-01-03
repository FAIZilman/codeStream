<script setup>
import { ChevronRight } from 'lucide-vue-next';
import { onMounted, reactive, useTemplateRef } from 'vue';

let allQuestion = useTemplateRef('questions');
// let answers = useTemplateRef('answers');

// questions.value.forEach(element => {
//     console.log(element)
// });

let faqs = reactive([
    {
        question: 'Apa itu website ini?',
        answer: 'Website ini dibuat sebagai media informasi dan pembelajaran yang bertujuan untuk membantu pengguna memahami fitur, layanan, dan konten yang tersedia. Selain itu, website ini juga berfungsi sebagai sarana untuk menampilkan hasil karya, project, atau informasi penting yang dapat diakses secara online dengan mudah.'
    },
    {
        question: 'Apakah website ini gratis untuk digunakan?',
        answer: 'Ya, website ini dapat digunakan secara gratis oleh semua pengguna. Kamu tidak perlu membayar biaya apa pun untuk mengakses konten utama yang tersedia. Namun, ke depannya mungkin akan ada fitur tambahan yang bersifat opsional.'
    },
    {
        question: 'Apakah saya perlu membuat akun untuk menggunakan website ini?',
        answer: 'Tidak, kamu tidak diwajibkan untuk membuat akun. Sebagian besar fitur dapat langsung digunakan tanpa proses pendaftaran. Hal ini bertujuan agar pengguna dapat mengakses informasi dengan cepat dan praktis.'
    },
    {
        question: 'Bagaimana cara menggunakan website ini?',
        answer: 'Cara menggunakan website ini sangat mudah. Kamu hanya perlu membuka halaman utama, lalu menavigasi menu yang tersedia sesuai dengan kebutuhanmu. Setiap halaman sudah dilengkapi dengan petunjuk yang jelas agar pengguna dapat memahami fungsi dan tujuan dari setiap fitur.'
    },
])
onMounted(() => {
    allQuestion.value.forEach((f) => {
        f.addEventListener('click', (e) => {
            e.currentTarget.classList.toggle('text-blue-500')
            e.currentTarget.children[0].classList.toggle('rotate-90')
            e.currentTarget.nextElementSibling.classList.toggle('max-h-0')
            e.currentTarget.nextElementSibling.classList.toggle('max-h-[500px]')
            e.currentTarget.nextElementSibling.classList.toggle('pb-4')
            allQuestion.value.forEach((l) => {
                if (l != f) {
                    l.classList.remove('text-blue-500')
                    l.children[0].classList.remove('rotate-90')
                    l.nextElementSibling.classList.remove('max-h-[500px]')
                    l.nextElementSibling.classList.add('max-h-0')
                    l.nextElementSibling.classList.remove('pb-4')
                }
            });
        });
    })
})
</script>

<template>
    <section id="services"
        class="relative overflow-hidden bg-gray-50 dark:bg-[#28282a] py-12 px-6 sm:px-8 md:px-10 lg:py-24 lg:px-24 grid justify-center transition-all duration-200 ease-in-out">
        <h1
            class="text-4xl sm:text-5xl text-gray-900 dark:text-slate-50 text-center mt-8 lg:mt-0 transition-all duration-300 ease-in-out font-bold">
            Faqs & Questions</h1>
        <div class="grid gap-y-3 mt-10">
            <div v-for="(faq, index) in faqs" :key="index"
                class="bg-gray-200 dark:bg-[#3c3c3c] dark:text-white rounded-xl">
                <h2 class="flex px-2 py-4  font-semibold" ref="questions">
                    <ChevronRight class="transition-all duration-350" />
                    {{ faq.question }}
                </h2>
                <div class="transition-all px-8 max-h-0 overflow-hidden duration-400 ease-in-out"
                    :id="`answer${index}`">
                    {{ faq.answer }}
                </div>
            </div>
        </div>
    </section>
</template>


<style scoped></style>
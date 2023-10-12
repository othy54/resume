<template>
    <header ref="header" class="section section-header -translate-y-[120%] transition-transform duration-300"
        :class="isSticky && 'header--hidden'">
        <div class="container flex justify-center items-center">
            <div>
                <nav class="bg-white bg-opacity-25  px-8 py-6 rounded-b-xl backdrop-blur-lg ">
                    <ul class="flex gap-10 lg:gap-20">
                        <li v-for="item in menuItems" :key="item">
                            <a class="text-white text-lg" :href="item.hash" :target="item.target">
                                {{ item.label }}
                            </a>
                        </li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>
</template>
<script setup>

import CV from '../assets/pdf/cv-othman-bensaoula.pdf'

const menuItems = ref([

    {
        label: 'Projets',
        hash: '#projects',
        target: ''
    },
    {
        label: 'CV',
        hash: CV,
        target: '_blank'
    },
    {
        label: 'LinkedIn',
        hash: 'https://www.linkedin.com/in/othman-bensaoula-dev/',
        target: '_blank'
    }

])
const header = ref(null);
const isSticky = ref(false);
const oldScroll = ref(0);
const hideHeader = () => {

    if (oldScroll.value < window.scrollY && window.scrollY > 150) {
        isSticky.value = true;
    } else if (oldScroll.value > window.scrollY) {
        isSticky.value = false;
    }

    oldScroll.value = window.scrollY;
}

onMounted(() => {
    window.addEventListener('scroll', hideHeader)
})

</script>
<style scoped>
.header--hidden {
    transform: translateY(-100%) !important
}
</style>
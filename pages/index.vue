<template>
    <div class="pb-20">
        <Header class="fixed w-full mt-4 z-[2]" />

        <!-- SECTION HERO -->

        <section class="section section-hero h-screen flex items-center w-full relative">
            <div class="row w-full">
                <div class="container">
                    <img class="mx-auto" width="300" height="300" src="~/assets/img/pp-othman.png"
                        alt="photo de profil Othman">
                    <div class="wrapper-title">
                        <h1 class="text-center text-white text-[72px]" split-text>
                            Othman Bensaoula
                        </h1>
                    </div>
                    <div class="wrapper-scroll uppercase absolute bottom-8 left-1/2 -translate-x-1/2 text-white">
                        <div class="scroll h-[60px] w-[1px] bg-white mx-auto mb-4"></div>
                        Scroll
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION PRESENTATION -->
        <section class="section section-prez h-screen flex items-center justify-center relative">
            <div class="row">
                <div class="container">
                    <div>
                        <div split-text class="text-center text-white text-5xl leading-[120%]">Hey ! Je suis Othman et je
                            suis
                            développeur
                            web front-end, très passionné par le code, je le vois comme un jeu et un challenge. Mon soucis
                            est de toujours fournir un code de qualité et optimisé, je suis interessé par le créative dev et
                            fournir les meilleures performances pour un site web.</div>
                    </div>
                    <div class="wrapper-scroll uppercase absolute bottom-8 left-1/2 -translate-x-1/2 text-white">
                        <div class="scroll h-[60px] w-[1px] bg-white mx-auto mb-4"></div>
                        Voir les projets
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION PROJETS -->

        <section id="projects" class="section section-projects">
            <div class="row">
                <div class="container">
                    <div v-for="project in projects" :key="project" class="wrapper-project group mb-80">
                        <hr>
                        <div class="flex group-even:flex-row-reverse mt-10 gap-10">
                            <img class=" w-2/3" :src="project.img" :alt="project.alt">
                            <div class="project-info pt-10 pb-4 flex flex-col justify-between">
                                <div>
                                    <h2 class="title text-white text-5xl group-even:text-right font-medium">
                                        {{ project.name }}
                                    </h2>
                                    <p class="mt-5 text-white text-2xl group-even:text-right">
                                        {{ project.stacks }}
                                    </p>
                                </div>
                                <div class="text-white group-even:text-right">
                                    <a rel="noopener no-follow" target="_blank" :href="project.link">{{ project.link }}</a>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
        </section>

    </div>
</template>
<script setup>

import SplitType from 'split-type';
const { $gsap } = useNuxtApp();
import Nancomcy from '../assets/img/projects/nancomcy.png'
import Aleo from '../assets/img/projects/aleo.png'

const projects = ref([
    {
        name: 'Nancomcy',
        stacks: 'Nuxt, Vue.js, GSAP, Tailwindcss',
        link: 'https://nancomcy.fr',
        img: Nancomcy,
        alt: 'screen nancomcy'
    },
    {
        name: 'ALEO',
        stacks: 'Nuxt, Vue.js, GSAP, Tailwindcss',
        link: 'https://aleo.agency',
        img: Aleo,
        alt: 'screen aleo'
    },
])


onMounted(() => {

    new SplitType('[split-text]', { types: 'words' });

    $gsap.to('.section-hero .word', {
        opacity: 1,
        y: 0,
        stagger: 0.08
    })

    const scrolls = document.querySelectorAll('.wrapper-scroll');
    scrolls.forEach((scroll) => {
        $gsap.to(scroll, {
            scrollTrigger: {
                trigger: scroll,
                scrub: true,
                start: 'top 80%',
                end: 'top 40%',
            },
            opacity: 0,
        })
    })


    $gsap.to('.section-prez .word', {
        scrollTrigger: {
            trigger: '.section-prez .container',
            start: 'top 60%',
        },
        opacity: 1,
        y: 0,
        stagger: 0.02
    });

    const projectEls = document.querySelectorAll('.wrapper-project');
    projectEls.forEach((project) => {
        $gsap.to(project.childNodes, {
            scrollTrigger: {
                trigger: project,
            },
            opacity: 0,
            stagger: 0.05,
        })
    })
})

</script>
<style>
.container {
    max-width: 1440px;
    margin: 0 auto;
}

.section {
    padding: 0 40px;

    @screen md {
        padding: 0 60px;
    }

    @screen lg {
        padding: 0 80px;
    }
}

.word {
    transform: translateY(100%);
}

.word {
    opacity: 0;
    transform: translateY(30%);
}
</style>
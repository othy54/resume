<template>
    <div class="pb-20">
        <div
            class="overlay-loader fixed z-50 w-full h-screen left-0 top-0 bg-slate-600 flex justify-center items-center text-white text-5xl">
            <h6>Loading ...</h6>
        </div>
        <div class="wrapper-three fixed w-full h-[100lvh] top-0 left-0"></div>
        <main class="relative">
            <Header class="fixed w-full z-[2]" />

            <!-- SECTION HERO -->

            <section class="section section-hero h-screen flex items-center w-full relative">
                <div class="row w-full">
                    <div class="container">
                        <img class="mx-auto pp-image opacity-0 w-[80%] lg:w-full max-w-[300px]" width="300" height="300"
                            src="~/assets/img/pp-othman.png" alt="photo de profil Othman">
                        <div class="wrapper-title">
                            <h1 class="text-center text-white text-[40px] lg:text-[72px] leading-[100%] mt-10" split-text>
                                Othman Bensaoula
                            </h1>
                        </div>
                        <div
                            class="wrapper-scroll uppercase absolute bottom-8 left-1/2 -translate-x-1/2 text-white opacity-0">
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
                            <div split-text class="text-center text-white text-2xl lg:text-5xl leading-[120%]">Hey ! Je suis
                                Othman et
                                je
                                suis
                                développeur
                                web front-end, très passionné par le code, je le vois comme un jeu et un challenge. Mon
                                souci
                                est de toujours fournir un code de qualité et optimisé, je suis interessé par le créative
                                dev et
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

            <section id="projects" class="section section-projects mt-40">
                <div class="row">
                    <div class="container">
                        <div v-for="project in projects" :key="project"
                            class="wrapper-project group mb-[20vh] lg:mb-[50vh] ">
                            <hr class="w-0 relative group-even:ml-auto">
                            <div class="flex flex-col lg:flex-row lg:group-even:flex-row-reverse mt-10 gap-4 lg:gap-10">
                                <img class="lg:w-2/3" :src="project.img" :alt="project.alt">
                                <div class="project-info pt-10 pb-4 flex flex-col justify-between">
                                    <div>
                                        <div class="overflow-hidden">
                                            <h2
                                                class="title text-white text-5xl lg:group-even:text-right font-medium translate-y-full">
                                                {{ project.name }}
                                            </h2>
                                        </div>
                                        <div class="overflow-hidden">
                                            <p
                                                class="w-full stacks mt-5 text-white text-2xl lg:group-even:text-right inline-block translate-y-full">
                                                {{ project.stacks }}
                                            </p>
                                        </div>
                                    </div>
                                    <div class="text-white lg:group-even:text-right overflow-hidden mt-10">
                                        <a class="inline-block translate-y-full link" rel="noopener no-follow"
                                            target="_blank" :href="project.link">{{ project.link }}</a>
                                    </div>
                                </div>
                            </div>
                        </div>

                    </div>
                </div>
            </section>
        </main>

    </div>
</template>
<script setup>

import SplitType from 'split-type';

const { $gsap } = useNuxtApp();

import Nancomcy from '../assets/img/projects/nancomcy.png'
import Aleo from '../assets/img/projects/aleo.png'
import Goddyns from '../assets/img/projects/goddyns.png'
import Tada from '../assets/img/projects/tada.png'
import Lapin from '../assets/img/projects/lapin.png'

import * as THREE from 'three';


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
    {
        name: "Goddyn's",
        stacks: 'Wordpress, Divi, Javascript',
        link: "https://www.goddyns.fr/",
        img: Goddyns,
        alt: 'screen goddyns'
    },
    {
        name: "Tada Ingénierie",
        stacks: 'Wordpress, Divi, GSAP',
        link: "https://tadaingenierie.fr/",
        img: Tada,
        alt: 'screen tadaingenierie'
    },
    {
        name: "Manipulation Threejs",
        stacks: 'Nuxt, Vue.js, Threejs, GSAP',
        link: "https://test-creative.netlify.app/threejs",
        img: Lapin,
        alt: 'screen lapin'
    },
])


const initThree = () => {
    let scene, camera, renderer;

    scene = new THREE.Scene();

    camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 1, 1000);
    camera.position.z = 1;
    camera.rotation.x = Math.PI / 2;

    renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.querySelector('.wrapper-three').appendChild(renderer.domElement);



    const animate = () => {
        renderer.render(scene, camera);
        requestAnimationFrame(animate);
    }

    animate();

    let starsGeometry = new THREE.BufferGeometry();
    let vertices = new Array(0);
    for (var i = 0; i < 6000; i++) {
        const x = THREE.MathUtils.randFloatSpread(2000);
        const y = THREE.MathUtils.randFloatSpread(2000);
        const z = THREE.MathUtils.randFloatSpread(2000);
        vertices.push(x, y, z);
    }
    starsGeometry.setAttribute('position', new THREE.Float32BufferAttribute(vertices, 3))
    const starsMaterial = new THREE.PointsMaterial({ color: 0x888888 });
    const starField = new THREE.Points(starsGeometry, starsMaterial);
    scene.add(starField);
}

const splitText = () => {
    new SplitType('[split-text]', { types: 'words' });
}

const gsapEffects = () => {

    $gsap.timeline().to('.overlay-loader', {
        y: '-100%',
        delay: 2
    }).to('header', {
        y: 0
    }).to('.pp-image', {
        opacity: 1
    }).to('.section-hero .word', {
        opacity: 1,
        y: 0,
        stagger: 0.08
    }).to('.wrapper-scroll', {
        opacity: 1,
        onComplete: () => {
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
        }

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
        $gsap.timeline({
            scrollTrigger: {
                trigger: project,
                start: 'top 70%'
            },
        }).to(project.querySelector('hr'), {
            width: '100%',
            ease: "power1.out",
        }).to(project.querySelector('img'), {
            clipPath: 'inset(0 0 0% 0)',
            ease: "power1.out",
            duration: 0.5,
        }, '>-0.3').to(project.querySelectorAll('.title, .stacks, .link'), {
            y: 0,
            stagger: 0.1
        })
    })
}


onMounted(() => {
    initThree();
    splitText();
    gsapEffects();

})

</script>
<style>
#projects {
    scroll-margin-top: 80px;
}

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

.wrapper-project {
    & img {
        clip-path: inset(0 0 100% 0);
    }
}
</style>
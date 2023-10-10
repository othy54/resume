<template>
    <header class="section">
        <div class="container flex justify-between items-center">
            <div>
                <img width="300" height="88" class="max-w-[200px] invert " src="~/assets/img/logo-othman.svg"
                    alt="logo othman">
            </div>
            <div>
                <nav>
                    <ul class="flex gap-10">
                        <li v-for="item in menuItems" :key="item">
                            <a class="text-white text-lg" :href="item.hash">
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

const menuItems = ref([
    // {
    //     label: 'Formations',
    //     hash: '#formations'
    // },
    {
        label: 'Projets',
        hash: '#projects'
    },
    // {
    //     label: 'Compétences',
    //     hash: '#skills'
    // },
    // {
    //     label: 'Autres',
    //     hash: '#others'
    // },

])

</script>
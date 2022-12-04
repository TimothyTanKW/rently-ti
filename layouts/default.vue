<script setup>
// apartment list
const { data: apartment } = await
useFetch(`https://6388cf94a4bb27a7f7925ef5.mockapi.io/apartment1`)

</script>
<template>
    <header>
        <div class="navbar bg-primary">
            <div class="flex-1 md:pl-6 pl-2">
                <NuxtLink to="/" class="normal-case text-3xl font-mono">RENTLY_TI</NuxtLink>
            </div>
            <div class="flex-none">
                <ul class="menu menu-horizontal p-0">
                    <li tabindex="0" class=" z-10">
                        <a>
                            Inventory
                            <svg class="fill-current" xmlns="http://www.w3.org/2000/svg" width="20" height="20"
                                viewBox="0 0 24 24">
                                <path d="M7.41,8.58L12,13.17L16.59,8.58L18,10L12,16L6,10L7.41,8.58Z" />
                            </svg>
                        </a>
                        <ul class="p-2 bg-base-100" >
                            <li v-for="apartment in apartment" :key="apartment.id"><NuxtLink :to="`/apartments/${apartment.id}`">{{apartment.propertyName}}</NuxtLink></li>
                        </ul>
                    </li>
                    <li><NuxtLink to="/">Home</NuxtLink></li>
                    
                </ul>
            </div>
        </div>
    </header>

    <div>
        <slot />
    </div>

    <footer class=" text-center pt-7 md:pt-20 pb-5 px-5 text-sm md:container mx-auto">
        <hr class="bg-gray-700 mb-2 border-gray-700">
        <p>©RentlyTI by Timothy</p>
    </footer>
</template>


<script>

</script>

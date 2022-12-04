<script setup>
// apartment list
const { data: apartment } = await
useFetch(`https://6388cf94a4bb27a7f7925ef5.mockapi.io/apartment1`)

</script>

<template>
  <div class="md:container md:mx-auto bg-base-100">
    <div class="flex items-center justify-between py-10 px-5">
      <h1 class="text-3xl">Apartment List</h1>
      <div class="text-lg">Total Listing : {{ apartment.length }}</div>
    </div>

    <div class="md:mx-auto justify-center md:mx-auto md:grid grid-cols-2 gap-x-10 gap-y-10  px-5 ">
      <div class="card lg:card-side bg-base-0 shadow-md max-w-3xl apartmentWrap bg-gray-700 rounded-xl mb-10 md:mb-0"
        v-for="apartment in apartment" :key="apartment.id">
         <figure class="w-full aprtName"> <img v-bind:src="apartment.image" alt="img" class="h-full" /></figure>
        <div class="card-body">
          <h2 class="card-title">{{ apartment.propertyName }}</h2>
          <p class="aprtAddress">{{ apartment.floor }}-{{ apartment.doorNumber }}, {{ apartment.address }}</p>
          <div class="card-actions justify-start pt-4">
            <button class="btn btn-primary h-10 px-5 text-sm border-none">
              <NuxtLink :to="`/apartments/${apartment.id}`">Inventory</NuxtLink>
            </button>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>


<script>
export default {
  name: 'homepage',
  el: '#aparmentListing',
}
</script>








  
  

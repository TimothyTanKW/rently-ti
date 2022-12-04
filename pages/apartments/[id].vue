<script setup>
const { id } = useRoute().params
const uri = 'https://6388cf94a4bb27a7f7925ef5.mockapi.io/apartment1/' + id

const { data: apartment } = await useFetch(uri, { key: id })

const { data: listOfItems } = await
new useFetch(`https://6388cf94a4bb27a7f7925ef5.mockapi.io/listofitems`)

</script>
<template>

  <div class="md:container md:mx-auto">
    <div class="py-10 px-5">
      <h1 class="text-3xl">{{ apartment.propertyName }}</h1>
      <h3> Details & Inventory List</h3>
    </div>
    <div class="lg:grid grid-cols-2">
      <figure class="w-full aprtName max-w-3xl grid-cols-2 gap-x-10 gap-y-10 sm:px-5"> <img class="sm:rounded-xl"
          v-bind:src="apartment.image" alt="img" /></figure>
      <div class="px-5 pt-5">
        <h4 class="text-lg"><strong>Address:</strong></h4>
        <p>{{ apartment.floor }}-{{ apartment.doorNumber }}, {{ apartment.address }}</p>

        <!-- Table -->

        <h4 class="text-lg pt-5"><strong>Inventory</strong></h4>
        <div class="overflow-x-auto pt-5">
          <table class="table w-full">
            <!-- head -->
            <thead>
              <tr>
                <th class="bg-gray-700 border-slate-800">Item</th>
                <th class="bg-gray-700 border-slate-800">Quantity</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(inventory, index) in inventories" :key="index">
                <td class="bg-gray-700 border-slate-800">{{ inventory.item }}</td>
                <td class="bg-gray-700 border-slate-800">{{ inventory.quantity }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <!-- The button to open modal -->
        <label for="my-modal" class="btn btn-primary h-10 px-5 text-sm border-none mt-10">UPDATE</label>
      </div>

    </div>




    <!-- Put this part before </body> tag -->
    <input type="checkbox" id="my-modal" class="modal-toggle" />
    <div class="modal">
      <div class="modal-box bg-slate-700">


        <!--lIST Outputs -->
        <div id="inventoryList">
          <h4 class="text-lg pt-5 pb-3"><strong>Add Items & Quantity</strong></h4>
          <div class="md:flex items-center">
            <select v-model="inventory" class="py-2 md:w-1/2 pl-3 w-3/4">
              <option disabled value="">Please select one</option>
              <option v-for="(listOfItems, index) in listOfItems" :value="listOfItems.item" :id="index">
                {{ listOfItems.item }}
              </option>
            </select>
            <input type="number" v-model="quantity" placeholder="1" v-on:keypress='numbersOnly' max="20"
              min="1" @input="() => { if (quantity > 150 || quantity < 0) { quantity = 20 } }"
              class="py-2 md:w-1/6 w-1/5 pl-3 ml-3" />

            <div class="modal-action mt-0 sm:pl-3 md:justify-end justify-start md:mt-0 mt-5">
              <label @click="submitInventory()" class="btn btn-primary h-10 px-5 text-sm border-none">
                ADD TO LIST
              </label>
            </div>
          </div>
        </div>


        <!-- Table -->

        <h4 class="text-lg pt-7"><strong>Preview Inventory List</strong></h4>
        <div class="overflow-x-auto pt-3">
          <table class="table w-full">
            <!-- head -->
            <thead>
              <tr>
                <th class="bg-gray-700">Item</th>
                <th class="w-2 bg-gray-700 border-slate-800">Quantity</th>
                <th class="w-2 bg-gray-700 border-slate-800">Edit</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(inventory, index) in inventories" :key="index">
                <td class="bg-gray-700 border-slate-800">{{ inventory.item }}</td>
                <td class="bg-gray-700 border-slate-800">{{ inventory.quantity }}</td>
                <td class="bg-gray-700 border-slate-800"><button @click="deleteInventory(index)">Delete</button></td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="modal-action justify-center">
          <label for="my-modal" class="btn btn-primary h-10 px-5 text-sm border-none mt-10">Approve</label>
        </div>
        
      </div>
    </div>
  </div>

</template>


<script>

export default {
  name: 'inventoryPage',
  el: '#inventoryList',
  data() {
    return {
      quantity: '1',

    }
  },
  methods: {
    numbersOnly(evt) {
      evt = (evt) ? evt : window.event;
      var charCode = (evt.which) ? evt.which : evt.keyCode;
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
        evt.preventDefault();;
      } else {
        return true;
      }
    },

  },

  data() {
    return {
      inventory: '',
      editInventory: null,
      inventories: []
    }
  },
  methods: {
    submitInventory() {
      if (this.inventory.length === 0) return;


      this.inventories.push({
        item: this.inventory,
        quantity: this.quantity
      })


      this.inventory = '';
      this.quantity = '1';
    },
    deleteInventory(index) {
      this.inventories.splice(index, 1);
    },
  }


};
</script>

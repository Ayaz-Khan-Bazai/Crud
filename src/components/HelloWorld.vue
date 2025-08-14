<script setup>
import { ref } from 'vue'

// Form inputs
const productId = ref('')
const productName = ref('')
const productPrice = ref('')

// Product list
const products = ref([])
const bgColor = ref('white') // default

// Add new product
function addProduct() {
  {
    products.value.push({
      id: productId.value,
      name: productName.value,
      price: productPrice.value,



      isEditing: false, // Add edit flag per product
    })

    // Clear inputs
    productId.value = ''
    productName.value = ''
    productPrice.value = ''
    
  }
}
let editicon = ""
// Toggle edit mode
function toggleEdit(product) {
  product.isEditing = !product.isEditing

}
function toggledelete(product, index) {
  product.id = ""
  product.name = ""
  product.price = ""
  products.value.splice(index, 1)

}
</script>

<template>
  <div class="flex justify-center content-center flex-wrap my-5">
    <div class="w-[900px] justify-center flex flex-col">

      <!-- Heading -->
      <div class="border-2 border-solid bg-gray-300">
        <h1 class="text-[18px] text-left m-5">Add a new Product</h1>
      </div>

      <!-- Form -->
      <div class="border-2 text-gray-500 border-solid p-2">
        <div class="flex py-5 gap-3 text-center justify-center items-center flex-wrap">
          <h1 class="text-[18px]">ID</h1>
          <input v-model="productId" class="rounded-[5px] p-2 border-2 border-solid" type="text" placeholder="Enter ID">

          <h1 class="text-[18px]">Name</h1>
          <input v-model="productName" class="rounded-[5px] p-2 border-2 border-solid" type="text"
            placeholder="Enter Name">

          <h1 class="text-[18px]">Price</h1>
          <input v-model="productPrice" class="rounded-[5px] p-2 border-2 border-solid" type="text"
            placeholder="Enter Price">

          <button @click="addProduct" class="px-5 py-3 border-2 border-solid rounded-2xl bg-blue-300 text-black">
            Add
          </button>
        </div>
      </div>

      <!-- Product Cards -->
      <div v-for="(product, index) in products" :key="index"
        class="items-center flex flex-row justify-around border p-4 bg-blue-100 rounded shadow mt-4 flex-wrap gap-3">


        <div class=" w-[600px] flex justify-evenly text-center border-r-2 border-black">

          <!-- ID -->
          <div class=" text-center">
            <p><strong>ID</strong></p>
            <span v-if="!product.isEditing">{{ product.id }}</span>
            <input v-else v-model="product.id" class="border-2 p-1 rounded" type="text">
          </div>

          <!-- Name -->
          <div class=" text-center">
            <p><strong>Name</strong></p>
            <span v-if="!product.isEditing">{{ product.name }}</span>
            <input v-else v-model="product.name" class="border-2 p-1 rounded" type="text">
          </div>

          <!-- Price -->
          <div class=" text-center">
            <p><strong>Price</strong></p>
            <span v-if="!product.isEditing">{{ product.price }}</span>
            <input v-else v-model="product.price" class="border-2 p-1 rounded" type="text">
          </div>

        </div>
        <!-- Edit/Save Button -->
        <div class=" flex gap-3 justify-self-end">

          <button @click="toggleEdit(product)" class="px-5 py-2 border-2 rounded-[6px] rounded-bl-4xl rounded-tr-4xl bg-green-700 text-white">
            {{ product.isEditing ? 'Save' : 'Edit' }}
          </button>
          <button @click="toggledelete(product)" class=" text-[18px] px-5 py-2 border-2 rounded-[6px] rounded-tr-4xl rounded-bl-4xl bg-red-700 text-white"> <i class="fa-solid fa-trash"></i>
          </button>
        </div>
      </div>

    </div>
  </div>
</template>

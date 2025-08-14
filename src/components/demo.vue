<script setup>
import { ref } from 'vue'

// Form inputs
const productId = ref('')
const productName = ref('')
const productPrice = ref('')

const edproductId = ref('')
const edproductName = ref('')
const edproductPrice = ref('')

// Array of all products
const products = ref([])



// Function to add a new product
function addProduct() {
    // if (productId.value && productName.value && productPrice.value) 
    {
        products.value.push({
            id: productId.value,
            name: productName.value,
            price: productPrice.value
        })

        edproductId.value = productId.value
        edproductName.value = productName.value
        edproductPrice.value = productPrice.value


        // Clear input        
        productId.value = ''
        productName.value = ''
        productPrice.value = ''
    }


}

const edititem = ref(false)

function editproducts() {
    
    edititem.value = !edititem.value
    // edproductId.value
    // edproductName.value 
    // edproductPrice.value
    

}



</script>

<template>
    <div class="flex justify-center content-center flex-wrap">
        <div class="w-[900px] justify-center flex flex-col">
            <!-- Heading -->
            <div class="border-2 border-solid bg-gray-300">
                <h1 class="text-[18px] text-left m-5">Add a new Product</h1>
            </div>

            <!-- Input Section -->
            <div class="border-2 text-gray-500 border-solid p-2">
                <div class="flex py-5 gap-3 text-center justify-center items-center flex-wrap">
                    <h1 class="text-[18px]">ID</h1>
                    <input v-model="productId" class="rounded-[5px] p-2 border-2 border-solid" type="text"
                        placeholder="Enter ID">

                    <h1 class="text-[18px]">Name</h1>
                    <input v-model="productName" class="rounded-[5px] p-2 border-2 border-solid" type="text"
                        placeholder="Enter Name">

                    <h1 class="text-[18px]">Price</h1>
                    <input v-model="productPrice" class="rounded-[5px] p-2 border-2 border-solid" type="text"
                        placeholder="Enter Price">

                    <button @click="addProduct"
                        class="px-5 py-3 border-2 border-solid rounded-2xl bg-blue-300 text-black">Add</button>
                </div>
            </div>

            <!-- Product Table -->
            <div cla v-for="(product, index) in products" :key="index"
                class=" items-center flex flex-row justify-around border p-4 bg-red-100 rounded shadow">

                <p><strong>ID:</strong><h1 v-if="edititem === false" class=" inline pl-2">{{ edproductId }}</h1></p>
                <input v-if="edititem" type="text" v-model="edproductId" class="border-2 border-solid" name="" id="">
                
                <p><strong>Name:</strong> <h1 v-if="edititem === false" class=" inline pl-2">{{ product.name }}</h1></p>
                <input v-if="edititem" type="text" v-model="edproductName" class="border-2 border-solid" name="" id="">

                <p><strong>Price:</strong> <h1 v-if="edititem === false" class=" inline pl-2">{{ product.price }}</h1></p>
                <input v-if="edititem" type="text" v-model="edproductPrice" class="border-2 border-solid" name="" id="">
                
                <button @click="editproducts"class="px-5 py-3 border-2 border-solid rounded-2xl bg-blue-300 text-black">{{edititem ? 'Save' : 'Edit'}}</button>
            </div>

        </div>
    </div>
</template>

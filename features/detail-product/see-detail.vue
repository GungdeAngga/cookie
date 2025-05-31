<!-- features/detail-product/see-detail.vue -->
<template>
  <div class="max-w-6xl mx-auto px-4 py-8">
    <!-- Breadcrumb -->
    <nav class="mb-6">
      <ol class="flex items-center space-x-2 text-sm text-gray-500">
        <li><NuxtLink to="/" class="hover:text-blue-600">Home</NuxtLink></li>
        <li>/</li>
        <li><span>{{ currentProduct.name }}</span></li>
      </ol>
    </nav>

    <!-- Product Detail -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
      <!-- Product Image -->
      <div class="space-y-4">
        <img 
          :src="currentProduct.image" 
          :alt="currentProduct.name"
          class="w-full h-[500px] object-cover rounded-lg shadow-lg"
        />
      </div>

      <!-- Product Info -->
      <div class="space-y-6">
        <div>
          <h1 class="text-3xl font-bold text-gray-900 mb-2">{{ currentProduct.name }}</h1>
          <div class="flex items-center space-x-4 mb-4">
            <div class="flex items-center">
              <div class="flex text-yellow-400">
                <svg v-for="i in 5" :key="i" class="w-5 h-5" :class="i <= productDetails.rating ? 'fill-current' : 'fill-gray-300'" viewBox="0 0 20 20">
                  <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/>
                </svg>
              </div>
              <span class="ml-2 text-gray-600">({{ productDetails.reviews }} reviews)</span>
            </div>
          </div>
        </div>

        <!-- Price -->
        <div class="border-t border-b py-4">
          <div class="text-3xl font-bold text-green-600">{{ productDetails.price }}</div>
          <div class="text-sm text-gray-500 mt-1">Free shipping on orders over $50</div>
        </div>

        <!-- Stock Status -->
        <div class="flex items-center space-x-2">
          <div class="w-3 h-3 rounded-full" :class="productDetails.inStock ? 'bg-green-500' : 'bg-red-500'"></div>
          <span :class="productDetails.inStock ? 'text-green-600' : 'text-red-600'">
            {{ productDetails.inStock ? 'In Stock' : 'Out of Stock' }}
          </span>
        </div>

        <!-- Description -->
        <div>
          <h3 class="text-lg font-semibold mb-2">Description</h3>
          <p class="text-gray-700 leading-relaxed">{{ productDetails.fullDescription }}</p>
        </div>

        <!-- Features -->
        <div>
          <h3 class="text-lg font-semibold mb-2">Key Features</h3>
          <ul class="list-disc list-inside space-y-1 text-gray-700">
            <li v-for="feature in productDetails.features" :key="feature">{{ feature }}</li>
          </ul>
        </div>

        <!-- Add to Cart Section -->
        <div class="space-y-4 pt-6">
          <div class="flex items-center space-x-4">
            <label class="text-sm font-medium">Quantity:</label>
            <select class="border border-gray-300 rounded-md px-3 py-2">
              <option v-for="i in 10" :key="i" :value="i">{{ i }}</option>
            </select>
          </div>
          
          <div class="flex space-x-4">
            <button 
              class="flex-1 bg-blue-600 text-white py-3 px-6 rounded-lg font-semibold hover:bg-blue-700 transition-colors"
              :disabled="!productDetails.inStock"
            >
              Add to Cart
            </button>
            <button class="px-6 py-3 border border-gray-300 rounded-lg hover:bg-gray-50 transition-colors">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
              </svg>
            </button>
          </div>
        </div>

        <!-- Specifications -->
        <div class="border-t pt-6">
          <h3 class="text-lg font-semibold mb-3">Specifications</h3>
          <dl class="space-y-2">
            <div v-for="spec in productDetails.specifications" :key="spec" class="flex">
              <dt class="text-gray-600 w-32">{{ spec.split(':')[0] }}:</dt>
              <dd class="text-gray-900">{{ spec.split(':')[1] }}</dd>
            </div>
          </dl>
        </div>
      </div>
    </div>

    <!-- Back Button -->
    <div class="mt-8">
      <NuxtLink 
        to="/" 
        class="inline-flex items-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50"
      >
        <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/>
        </svg>
        Back to Products
      </NuxtLink>
    </div>
  </div>
</template>

<script setup lang="ts">
import { product } from '~/features/home-page/constant/product'

// Get the product ID from the route
const route = useRoute()
const productId = route.params.productName
const currentProduct = product.find(item => item.name === productId)

// If product not found, show 404 or redirect
if (!currentProduct) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Product not found'
  })
}

// You can add more product details here
const productDetails = {
  ...currentProduct,
  price: '$29.99', // Add price
  rating: 4.5, // Add rating
  reviews: 128, // Add review count
  inStock: true, // Stock status
  fullDescription: currentProduct.desc,
  specifications: [
    'Material: Premium Quality',
    'Weight: 1.2 kg',
    'Dimensions: 20 x 15 x 5 cm',
    'Warranty: 2 years'
  ],
  features: [
    'Eco-friendly materials',
    'Easy to use',
    'Durable construction',
    'Modern design'
  ]
}
</script>
<template>
    <div class="grid grid-cols-12 gap-4">
        <div v-for="item in product" :key="item.name" class="flex flex-col col-span-3 w-full">
            <img :src="item.image" :alt="item.name"/>
            <div class="bg-red-200 flex flex-col">
                <span>{{ item.name }}</span>
                <button>add to cart</button>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { product } from './constant/product'
</script>
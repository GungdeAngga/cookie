<template>
    <div class="grid grid-cols-12 gap-4">
        <div v-for="item in product" :key="item.name" class="flex flex-col col-span-12 md:col-span-6 lg:col-span-3 w-full">
            <img :src="item.image" :alt="item.name" class="rounded-t-lg"/>
            <div class="bg-gray-200 flex flex-col p-3 pt-2 space-y-3 rounded-b-lg">
                <span class="font-bold text-xl">{{ item.name }}</span>
                <span>{{ item.desc?.slice(0, 30) }}...</span>
                <NuxtLink 
                    :to="`/detail/${item.name}`"
                    class="bg-green-600 text-white rounded-md py-2 px-4 text-center hover:bg-green-700 transition-colors"
                >
                    See Detail
                </NuxtLink>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { product } from './constant/product'
</script>
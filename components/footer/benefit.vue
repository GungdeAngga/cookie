<template>
    <div class="flex flex-col">
        <span class="font-bold text-xl pb-2">E-commerce benefit</span>
        <div v-for="benefit in benefits" :key="benefit.id" class="flex space-x-3 space-y-1">
            <img :src="benefit.icon" class="w-6 h-6 invert"/>
            <span>{{ benefit.title }}</span>
        </div>
    </div>
</template>

<script setup lang="ts">
import { benefits } from './constant/benefit'
</script>
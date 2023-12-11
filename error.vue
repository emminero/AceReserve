<template>
    <div>   
        <div class="mx-auto w-1/2 flex justify-center pt-10">
            <div class="border w-full text-center py-10 shadow-lg space-y-4">
                <p class="font-bold text-7xl">{{ error.statusCode }}</p>
                <p class="text-6xl">Oops</p>
                <p>{{ error.message }}</p>
            </div>
        </div>
    </div>
</template>
<script setup>
    defineProps(['error'])
</script>
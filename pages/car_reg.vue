<template>
    <div class="font-poppins m-10">
        <header class="flex justify-between">
            <div>
                <h1 class="text-3xl my-2 font-semibold">Car Registration</h1>
                <p class="my-2">Fill the form below to complete your car registration</p>
            </div>

            <button class="bg-black text-white px-6 h-9 rounded-full justify-end btn">
                <Nuxtlink>Register</Nuxtlink>
            </button>
        </header>
        <h1 class="mb-8 mt-3 text-3xl ">Car Details</h1>

        <div class="grid grid-cols-2">
            <form class="mr-8">
                <label for="car-model" class="block font-medium">Car Model</label>
                <input type="text" id="car-model" class="mt-1 p-2 border-2 border-gray-400 rounded-md w-full mb-5">

                <label for="engine-number" class="block font-medium">Engine Number</label>
                <input type="text" id="engine-number" class="mt-1 p-2 border-2 border-gray-400 rounded-md w-full mb-5">

                <label for="car-colour" class="block font-medium">Car Colour</label>
                <input type="text" id="car-colour" class="mt-1 p-2 border-2 border-gray-400 rounded-md w-full mb-5">

                <label for="plate-number" class="block font-medium">Plate Number</label>
                <input type="text" id="plate-number" class="mt-1 p-2 border-2 border-gray-400 rounded-md w-full mb-5">

                <label for="custom-clear" class="block font-medium">Custom Clearance Number</label>
                <input type="text" id="custom-clear" class="mt-1 p-2 border-2 border-gray-400 rounded-md w-full mb-5">

            </form>

            <div>
                <div class="text-center text-gray-700 text-sm">
                    <p class="mb-3">Upload your car image in SVG</p>
                    <p>Only upload in SVG</p>
                </div>
                
                <div class="w-[550px] h-[320px] border-dashed border-4 border-gray-400 my-7 flex items-center justify-center rounded">
                    <img src="/assets/images/image.png" alt="image" class="max-w-full max-h-full object-contain h-48">
                </div>

                <div class="flex justify-center">
                    <button class="bg-black text-white px-16 text-sm h-9 rounded-full justify-end btn">Choose file</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>

</style>
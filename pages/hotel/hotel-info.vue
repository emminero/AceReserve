<template>
    <div>
        <section class="bg-[#121201]">
            <div class="py-16 w-5/6 mx-auto">
                <h1 class="text-white text-center text-2xl font-semibold">Details about Oriental Hotels and Suite</h1>
            </div>
        </section>

        <section>
            <div class="w-5/6 mx-auto py-16">
                <div class="flex justify-between">
                    <div class="w-1/2 border rounded">
                        <div class="h-[400px]">
                            <img :src="room" width="600" height="600" class="object-fit" alt="Room Image">
                        </div>
                        <div class="mt-5">
                            <ul class="px-4 space-y-4">
                                <li>24 Hours Electricity</li>
                                <li>Parking Lot</li>
                                <li>Spa</li>
                                <li>Security Guard</li>
                                <li>WiFi Internet Access</li>
                            </ul>
                        </div>
                    </div>
                    <div class="w-1/3">
                        <div class="py-4 px-3 border rounded-md">
                            <span class="text-center block text-lg font-semibold">Book rooms at Oriental Hotel and Suite</span>
                            <div class="pt-10 space-y-6 font-medium">
                                <div>
                                    <label for="check-in">Check-in</label>
                                    <input type="date" name="date" id="check-in" class="block bg-[#121201] text-white w-full px-4 py-3">
                                </div>
                                <div>
                                    <label for="check-out">Check-out</label>
                                    <input type="date" name="date" id="check-out" class="block bg-[#121201] text-white w-full px-4 py-3">
                                </div>
                                <div>
                                    <label for="check-out">Number of rooms</label>
                                    <input type="number" name="number" id="check-out" value="1" class="block bg-[#121201] text-white w-full px-4 py-3">
                                </div>
                                <div>
                                    <label for="check-out">Number of People</label>
                                    <input type="number" name="number" id="check-out" value="1" class="block bg-[#121201] text-white w-full px-4 py-3">
                                </div>
                                <div>
                                    <label for="check-out">Email (Optional)</label>
                                    <input type="email" name="number" id="check-out" value="james@example.com" class="block bg-[#121201] text-white w-full px-4 py-3">
                                </div>
                                <div>
                                    <label for="check-out">Amount</label>
                                    <input type="text" name="number" id="check-out" value="20000" class="block bg-[#121201] text-white w-full px-4 py-3">
                                </div>
                                <div class="pt-10">
                                    <NuxtLink to="/checkout" class="w-full block bg-[#DB822F] rounded-[30px] py-3 text-center font-medium text-white">Proceed</NuxtLink>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script setup>
const room = ref('')

room.value = 'https://images.unsplash.com/photo-1598928506311-c55ded91a20c?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OHx8cm9vbXxlbnwwfHwwfHx8MA%3D%3D'
</script>

<style scoped>
input[type="date"]::-webkit-calendar-picker-indicator {
    background-color: gray;
    cursor: pointer;
}
</style>
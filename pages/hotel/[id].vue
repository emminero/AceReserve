<template>
    <div v-if="dataReady">
        <section class="bg-[#121201]">
            <div class="py-16 w-5/6 mx-auto">
                <h1 class="text-white text-center text-2xl font-semibold">Details about {{ data['details']['name'] }}</h1>
            </div>
        </section>

        <section>
            <div class="w-1/2 mx-auto">
                <img :src="data['details']['image']" class="w-full" alt="A picture of this hotel">
            </div>
        </section>

        <section>
            <div class="w-5/6 mx-auto py-16">
                <div class="flex justify-between">
                    <div class="w-1/2 border rounded">
                        <div>
                            <div class="border h-[420px]">
                                <Splide :options="{ type:loop,autoplay:true,interval:2500,rewind:true}" aria-label="My Favorite Images">
                                    <SplideSlide v-for="(images, index) in data['details']['images']" :key="index">
                                        <img :src="images" class="w-full h-full" alt="hotel 1">
                                    </SplideSlide>
                                </Splide>
                            </div>

                            <div class="mt-5 flex justify-between">
                                <button class="bg-[#121201] text-white px-6 py-3">View With AR</button>
                                <button class="bg-[#121201] text-white px-6 py-3">Live Map</button>
                            </div>
                        </div>  
                        <div class="mt-5">
                            <div class="px-4 space-y-4">
                                <h1 class="text-center font-semibold text-lg">Details</h1>
                                <div>
                                    <span class="font-semibold">Location: </span><span>{{ data['details']['location'] }}, {{ data['details']['state'] }}, Nigeria</span>
                                </div>
                                <div>
                                    <span class="font-semibold">Type: </span><span>{{ data['details']['type'] }}</span>
                                </div>
                                <div>
                                    <span class="font-semibold">Rating: </span><span>{{ data['details']['rating'] }}</span>
                                </div>
                                <div>
                                    <span class="font-semibold">Star: </span><span>{{ data['details']['star'] }} Stars</span>
                                </div>
                                <div>
                                    <span class="font-semibold">Reviews: </span><span>{{ data['details']['review'] }} Reviews</span>
                                </div>
                                <h1 class="text-center font-semibold text-lg">Room Types</h1>
                                <div v-for="(room, key) in  data['details']['roomTypes']" :key="key">
                                    <span>{{ room['type']  }}: </span><span class="font-semibold text-sm">&#8358;{{ room['price'] }} ({{ room['availability'] ? 'Available' : 'Not Available' }})</span>
                                </div>
                                <h1 class="text-center font-semibold text-lg">Facilities</h1>
                                <div>
                                    <span>{{ data['details']['breakfast'] ? 'Breakfast Available' : '' }} </span>
                                </div>
                                <div>
                                    <span>{{ data['details']['freeWifi'] ? 'FreeWifi Available' : '' }} </span>
                                </div>
                                <div>
                                    <span>{{ data['details']['parkingLot'] ? 'Parking Lot Available' : '' }} </span>
                                </div>
                                <div>
                                    <span>{{ data['details']['reception'] ? 'Reception Available' : '' }} </span>
                                </div>
                                <div>
                                    <span>{{ data['details']['swimmingPool'] ? 'Swimming Pool Available' : '' }}  </span>
                                </div>
                            </div>
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
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'
import { Splide, SplideSlide } from '@splidejs/vue-splide';


const { $web5: web5, $myDID: myDID } = useNuxtApp();
const room = ref('')
const companyDID = ref('')
const data = ref([])
const dataReady = ref(false)


room.value = 'https://images.unsplash.com/photo-1598928506311-c55ded91a20c?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OHx8cm9vbXxlbnwwfHwwfHx8MA%3D%3D'
const { id } = useRoute().params
companyDID.value = "did:ion:EiD23C68csobyUtnDDRwyu8QjaqhCSMGAIgs_ID6ScE_WQ:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJkd24tc2lnIiwicHVibGljS2V5SndrIjp7ImNydiI6IkVkMjU1MTkiLCJrdHkiOiJPS1AiLCJ4IjoiQmJtUFl3UDBNSzRSLUVYcUlxSGxnRENhV0ZmS1drWndPX29SU0szT1dZVSJ9LCJwdXJwb3NlcyI6WyJhdXRoZW50aWNhdGlvbiJdLCJ0eXBlIjoiSnNvbldlYktleTIwMjAifSx7ImlkIjoiZHduLWVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJIb3NtcDZxRll0a281VUM0dU9YQTEzcUVuVjBNVlljVFp0R05FSkpHYlpvIiwieSI6Im9qMmVSVzhJSUNKSmdjQnJZUUNmN3ZGNHp0eTJFbV9nOWx1TzVubDJMajgifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7ImVuY3J5cHRpb25LZXlzIjpbIiNkd24tZW5jIl0sIm5vZGVzIjpbImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduMyIsImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduMCJdLCJzaWduaW5nS2V5cyI6WyIjZHduLXNpZyJdfSwidHlwZSI6IkRlY2VudHJhbGl6ZWRXZWJOb2RlIn1dfX1dLCJ1cGRhdGVDb21taXRtZW50IjoiRWlCYldkYl9xNldBbVoxQ2RaN2lRdU1odVRKMEZ0OWRjZ2twYWRfUmhqSFpxUSJ9LCJzdWZmaXhEYXRhIjp7ImRlbHRhSGFzaCI6IkVpQVFCSXBjUWdCbEcydnNYNFgxRmtvMFgtR1YxeW5kNEVMNV9qVmVDVmdxRnciLCJyZWNvdmVyeUNvbW1pdG1lbnQiOiJFaUF6S25hcE16TkxfWm1hNFFvUkE0VlNZUnY1T1hNNWVycThOZ3BMOXJRZFpnIn19"


const getRecords = async() => {
    try {
        const { record } = await web5.dwn.records.read({
            from: companyDID.value,
            message: {
                filter: {
                    recordId: id
                },
            }
        });

        data.value = await record.data.json()
    } catch (e) {
        console.error(e)
        return
    }
}

onBeforeMount(async () => {
    await getRecords()

    dataReady.value = true;

    if(data.value.length) {
        throw createError({
            statusCode: 404,
            statusMessage: 'Page Not Found'
        })
    }
})
</script>

<style scoped>
input[type="date"]::-webkit-calendar-picker-indicator {
    background-color: gray;
    cursor: pointer;
}
</style>
<template>
    <div>
        <section class="bg-[#121201] ">
            <div class="w-5/6 mx-auto py-8">
                <div class="grid grid-cols-4 gap-x-10 justify-between">
                    <div>
                        <span class="text-gray-200 mb-2 block">Location</span>
                        <div class="flex py-2 bg-[#D8D8D8]">
                            <img src="~/assets/images/svg/locator.svg" alt="Location SVG">
                            <input type="text" class="border-none outline-none focus:none bg-transparent px-4" placeholder="Lagos">
                        </div>
                    </div>
                    <div>
                        <span class="text-gray-200 mb-2 block">Check-in</span>
                        <input type="date" class="border-none outline-none focus:none bg-[#D8D8D8] px-4 w-full  py-2">
                    </div>
                    <div>
                        <span class="text-gray-200 mb-2 block">Check-out</span>
                        <input type="date" class="border-none outline-none focus:none bg-[#D8D8D8] w-full px-4 py-2">
                    </div>
                    <div class="flex justify-center items-end">
                        <button @click="search" class="w-4/5 py-2 bg-[#DB822F] text-gray-200 hover:bg-orange-400 duration-300">Search</button>
                    </div>
                </div>
            </div>
        </section>

        <section>
            <div class="py-16 mx-auto w-5/6">
                <h1 class="text-center font-semibold text-3xl mb-5">Lagos: 81 Hotels Found</h1>
                <div class="flex justify-between gap-x-10">
                    <div class="w-1/5">
                        <div class="border border-b-0 rounded-lg">
                            <div class="border-b py-4 px-2">
                                <h1 class="font-semibold">Filter By:</h1>
                            </div>
                            <div class="border-b py-4 px-2">
                                <span class="font-semibold">Ratings</span>
                                <div class="mt-4 space-y-2 text-sm">
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="ratings" id="2star" value="1star" >
                                            <label for="2star" class="inline-block">2 stars</label>
                                        </div>
                                        <span class="block">12</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="ratings" id="3star" value="1star" >
                                            <label for="3star" class="inline-block">3 stars</label>
                                        </div>
                                        <span class="block">8</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="ratings" id="4star" value="1star" >
                                            <label for="4star" class="inline-block">4 stars</label>
                                        </div>
                                        <span class="block">56</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="ratings" id="5star" value="1star" >
                                            <label for="5star" class="inline-block">5 stars</label>
                                        </div>
                                        <span class="block">10</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="ratings" id="unrated" value="1star" >
                                            <label for="unrated" class="inline-block">Unrated</label>
                                        </div>
                                        <span class="block">24</span>
                                    </div>
                                </div>
                            </div>
                            <div class="border-b rounded-lg py-4 px-2">
                                <span class="font-semibold">Facilities</span>
                                <div class="mt-4 space-y-2 text-sm">
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="facilities" id="freewifi" value="freewifi" >
                                            <label for="freewifi" class="inline-block">Free Wifi</label>
                                        </div>
                                        <span class="block">13</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="facilities" id="parking" value="freewifi" >
                                            <label for="parking" class="inline-block">Parking Lot</label>
                                        </div>
                                        <span class="block">30</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="facilities" id="swimming" value="freewifi" >
                                            <label for="swimming" class="inline-block">Swimming Pool</label>
                                        </div>
                                        <span class="block">29</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="facilities" id="restaurant" value="freewifi" >
                                            <label for="restaurant" class="inline-block">Restaurant</label>
                                        </div>
                                        <span class="block">5</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center justify-between space-x-2">
                                            <input type="checkbox" name="facilities" id="spa" value="freewifi" >
                                            <label for="spa" class="inline-block">SPA</label>
                                        </div>
                                        <span class="block">2</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="w-4/5 space-y-10">
                        <div v-show="hotels" v-for="(hotel, index) in hotels" :key="index" class="border-t shadow-lg rounded-lg p-4 flex justify-between h-[250px] space-x-5">
                            <div class="w-1/3">
                                <img :src="hotel['data']['details']['image']" alt="Hotel Image" class="w-full h-full object-fit rounded-lg">
                            </div>
                            <div class="w-1/2">
                                <div class="h-2/5"> 
                                    <h1 class="text-2xl font-medium">{{ hotel['data']['details']['name'] }}</h1>

                                    <span class="text-sm">{{ hotel['data']['details']['location'] }}, {{ hotel['data']['details']['state'] }} state </span>
                                </div>
                                <div class="h-2/5 space-y-1">
                                    <div class="flex space-x-1 items-center">
                                        <span class="font-semibold text-sm">Type:</span><span class="font-medium text-sm">{{ hotel['data']['details']['type'] }}</span>
                                    </div>
                                    <div class="flex space-x-1 items-center">
                                        <span class="font-semibold text-sm">Reviews:</span><span class="font-medium text-sm">{{ hotel['data']['details']['review'] }}</span>
                                    </div>
                                    <div class="flex space-x-1 items-center">
                                        <span class="font-semibold text-sm">Ratings:</span><span class="font-medium text-sm">{{ hotel['data']['details']['rating'] }}</span>
                                    </div>
                                    <div class="flex space-x-1 items-center">
                                        <span class="font-semibold text-sm">Star:</span><span class="font-medium text-sm">{{ hotel['data']['details']['star'] }} Stars</span>
                                    </div>
                                </div>
                                <div class="h-1/5 flex flex-col pt-2">
                                    <div class="flex space-x-1">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-2.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                    </div>
                                    <div class="flex gap-3 mt-2">
                                        <span class="text-xs block font-semibold">
                                            {{ hotel['data']['details']['breakfast'] ? 'Breakfast' : null }} 
                                        </span>
                                        <span class="text-xs block font-semibold">
                                            {{ hotel['data']['details']['freeWifi'] ? 'FreeWifi' : null }} 
                                        </span>
                                        <span class="text-xs block font-semibold">
                                            {{ hotel['data']['details']['parkingLot'] ? 'Parking Lot' : null }} 
                                        </span>
                                        <span class="text-xs block font-semibold">
                                            {{ hotel['data']['details']['reception'] ? '24h Reception' : null }} 
                                        </span>
                                        <span class="text-xs block font-semibold">
                                            {{ hotel['data']['details']['swimmingPool'] ? 'Swimming Pool' : null }} 
                                        </span>
                                    </div>
                                </div>
                            </div>
                            <div class="w-1/5">
                                <div class="flex h-1/5 items-end justify-end">
                                    <span class="text-2xl text-[#DB822F]">&#8358;80,000</span><span class="text-xs">/Per night</span>
                                </div>
                                <div class="flex h-4/5 items-end justify-end">
                                    <NuxtLink :to="'/hotel/' + hotel['id']" class="bg-[#DB822F] px-6 py-3 text-white font-medium">Book Now</NuxtLink>
                                </div>
                            </div>
                        </div>
                        <div class="border-t shadow-lg rounded-lg p-4 flex justify-between h-[220px] space-x-5">
                            <div class="w-1/3">
                                <img :src="img" alt="Hotel Image" class="w-full h-full object-fit rounded-lg">
                            </div>
                            <div class="w-2/5">
                                <div class="h-4/5"> 
                                    <h1 class="text-2xl font-medium">Oriental Hotels and Suite</h1>

                                    <span class="text-sm">56 Taiwo Adeyanju close, Shomolu, Lagos state </span>
                                </div>
                                <div class="h-1/5 flex items-end">
                                    <div class="flex space-x-1">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-2.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                    </div>
                                </div>
                            </div>
                            <div class="w-1/3">
                                <div class="flex h-1/5 items-end justify-end">
                                    <span class="text-2xl text-[#DB822F]">&#8358;80,000</span><span class="text-xs">/Per night</span>
                                </div>
                                <div class="flex h-4/5 items-end justify-end">
                                    <NuxtLink to="/hotel/hotel-info" class="bg-[#DB822F] px-6 py-3 text-white font-medium">Book Now</NuxtLink>
                                </div>
                            </div>
                        </div>
                        <div class="border-t shadow-lg rounded-lg p-4 flex justify-between h-[220px] space-x-5">
                            <div class="w-1/3">
                                <img :src="img" alt="Hotel Image" class="w-full h-full object-fit rounded-lg">
                            </div>
                            <div class="w-2/5">
                                <div class="h-4/5"> 
                                    <h1 class="text-2xl font-medium">Sunshine Hotels and Suite</h1>

                                    <span class="text-sm">56 Taiwo Adeyanju close, Shomolu, Lagos state </span>
                                </div>
                                <div class="h-1/5 flex items-end">
                                    <div class="flex space-x-1">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-2.svg" alt="Star Ratings">
                                    </div>
                                </div>
                            </div>
                            <div class="w-1/3">
                                <div class="flex h-1/5 items-end justify-end">
                                    <span class="text-2xl text-[#DB822F]">&#8358;20,000</span><span class="text-xs">/Per night</span>
                                </div>
                                <div class="flex h-4/5 items-end justify-end">
                                    <button class="bg-[#DB822F] px-6 py-3 text-white font-medium">Book Now</button>
                                </div>
                            </div>
                        </div>
                        <div class="border-t shadow-lg rounded-lg p-4 flex justify-between h-[220px] space-x-5">
                            <div class="w-1/3">
                                <img :src="img" alt="Hotel Image" class="w-full h-full object-fit rounded-lg">
                            </div>
                            <div class="w-2/5">
                                <div class="h-4/5"> 
                                    <h1 class="text-2xl font-medium">Ace Hotels</h1>

                                    <span class="text-sm">56 Taiwo Adeyanju close, Shomolu, Lagos state </span>
                                </div>
                                <div class="h-1/5 flex items-end">
                                    <div class="flex space-x-1">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-1.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                        <img src="~/assets/images/svg/star-3.svg" alt="Star Ratings">
                                    </div>
                                </div>
                            </div>
                            <div class="w-1/3">
                                <div class="flex h-1/5 items-end justify-end">
                                    <span class="text-2xl text-[#DB822F]">&#8358;1,000,000</span><span class="text-xs">/Per night</span>
                                </div>
                                <div class="flex h-4/5 items-end justify-end">
                                    <button class="bg-[#DB822F] px-6 py-3 text-white font-medium">Book Now</button>
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


const { $web5: web5, $myDID: myDID } = useNuxtApp();
const img = ref('')
const companyDID = ref('')
const hotels = ref([])

companyDID.value = "did:ion:EiD23C68csobyUtnDDRwyu8QjaqhCSMGAIgs_ID6ScE_WQ:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJkd24tc2lnIiwicHVibGljS2V5SndrIjp7ImNydiI6IkVkMjU1MTkiLCJrdHkiOiJPS1AiLCJ4IjoiQmJtUFl3UDBNSzRSLUVYcUlxSGxnRENhV0ZmS1drWndPX29SU0szT1dZVSJ9LCJwdXJwb3NlcyI6WyJhdXRoZW50aWNhdGlvbiJdLCJ0eXBlIjoiSnNvbldlYktleTIwMjAifSx7ImlkIjoiZHduLWVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJIb3NtcDZxRll0a281VUM0dU9YQTEzcUVuVjBNVlljVFp0R05FSkpHYlpvIiwieSI6Im9qMmVSVzhJSUNKSmdjQnJZUUNmN3ZGNHp0eTJFbV9nOWx1TzVubDJMajgifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7ImVuY3J5cHRpb25LZXlzIjpbIiNkd24tZW5jIl0sIm5vZGVzIjpbImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduMyIsImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduMCJdLCJzaWduaW5nS2V5cyI6WyIjZHduLXNpZyJdfSwidHlwZSI6IkRlY2VudHJhbGl6ZWRXZWJOb2RlIn1dfX1dLCJ1cGRhdGVDb21taXRtZW50IjoiRWlCYldkYl9xNldBbVoxQ2RaN2lRdU1odVRKMEZ0OWRjZ2twYWRfUmhqSFpxUSJ9LCJzdWZmaXhEYXRhIjp7ImRlbHRhSGFzaCI6IkVpQVFCSXBjUWdCbEcydnNYNFgxRmtvMFgtR1YxeW5kNEVMNV9qVmVDVmdxRnciLCJyZWNvdmVyeUNvbW1pdG1lbnQiOiJFaUF6S25hcE16TkxfWm1hNFFvUkE0VlNZUnY1T1hNNWVycThOZ3BMOXJRZFpnIn19"
img.value = "https://media.istockphoto.com/id/1454662719/photo/african-american-tourists-with-suitcases-in-front-of-the-rented-apartment.webp?b=1&s=170667a&w=0&k=20&c=0gDMkmXBYiwcQ3Gc9loQ7--kaN38Wb9UQWWSSw8czqE="

const getRecords = async() => {
    console.log(companyDID.value)
    try {
        const { records } = await web5.dwn.records.query({
            from: companyDID.value,
            message: {
                filter: {
                    protocolPath: 'hotelDetails'
                },
            }
        });

        // console.log(records)

        for (let record of records) {
            const data = await record.data.json();
            const list = { data, id: record.id};
            hotels.value.push(list)
        }
    } catch (e) {
        console.error(e)
        return
    }
}

async function search() {
    await getRecords()
}

function slugify(str) {
  return String(str)
    .normalize('NFKD') // split accented characters into their base characters and diacritical marks
    .replace(/[\u0300-\u036f]/g, '') // remove all the accents, which happen to be all in the \u03xx UNICODE block.
    .trim() // trim leading or trailing whitespace
    .toLowerCase() // convert to lowercase
    .replace(/[^a-z0-9 -]/g, '') // remove non-alphanumeric characters
    .replace(/\s+/g, '-') // replace spaces with hyphens
    .replace(/-+/g, '-'); // remove consecutive hyphens
}

</script>

<template>
    <div class="w-4/5 mx-auto flex justify-center items-center py-10">
        <div class="w-full md:w-1/2 flex flex-col justify-center p-4 h-[500px]">

            <textarea v-model="recordId" class="border border-black rounded-sm mt-2 w-full h-3/5 p-2 block" placeholder="Input your record Id"></textarea>
            <p class="text-md text-center font-semibold text-red-600">{{ error }}</p>
            <button @click="check" class="bg-black text-white mt-2 inline py-2 ">Check Bookings</button>
        </div>
    </div>

    <div class="max-w-full overflow-hidden"> 
            {{ read }}
        </div>
</template>

<script setup>

import { VerifiableCredential } from '@web5/credentials';
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'

const { $web5: web5, $myDID: myDID } = useNuxtApp();
const error = ref('')
const recordId = ref('')
const bookings = ref([])
const read = ref([])


async function check(){
    if(recordId.value)
    {
        let { record } = await web5.dwn.records.read({
            message: {
                filter: {
                    recordId: recordId.value
                }
            }
        })

        const data = await record.data.text();
        read.value = VerifiableCredential.parseJwt(data)
        console.log(read.value)

    }else {
        error.value = "Input your DID"
    }
}
</script>
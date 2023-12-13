<template>
    <div class="w-4/5 mx-auto flex justify-center items-center py-10">
        <div class="w-full md:w-1/2 flex flex-col justify-center p-4 h-[500px]">

            <textarea v-model="userDID" class="border border-black rounded-sm mt-2 w-full h-3/5 p-2 block" placeholder="Input your DID"></textarea>
            <p class="text-md text-center font-semibold text-red-600">{{ error }}</p>
            <button @click="check" class="bg-black text-white mt-2 inline py-2 ">Check Bookings</button>
        </div>

        <div>
            {{ bookings }}
        </div>
    </div>
</template>

<script setup>

import { VerifiableCredential } from '@web5/credentials';
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'

const { $web5: web5, $myDID: myDID } = useNuxtApp();
const error = ref('')
const userDID = ref('')
const bookings = ref([])


async function check(){
    if(userDID.value)
    {
        const { records } = await web5.dwn.records.query({
            from: userDID.value,
            message: {
                filter: {
                    dataFormat: 'application/vc+jwt',
                    protocolPath: "bookedRooms",
                    schema: hotelReservationProtocol.types.bookedRooms.schema,
                    protocol: hotelReservationProtocol.protocol,
                },
            }
        });

        for (let record of records) {
            const data = VerifiableCredential.parseJwt(await record.data.text());
            const list = { data, id: record.id};
            bookings.value.push(list)
        }
    }else {
        error.value = "Input your DID"
    }
}
</script>
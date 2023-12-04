<template>
    <div>
        <div class="w-4/5 mx-auto border p-4 flex justify-between">
            <input type="text" class="border border-gray-400 px-4 py-2 rounded-md" placeholder="Which Location?">
            <button @click="search()" class="rounded-md hover:bg-black text-white px-6 py-2 bg-gray-800">Search</button>
        </div>
    </div>

    <div>
        <div class="w-4/5 mt-10 mx-auto flex gap-4" v-for="(value, key) in hotels" :key="key">
            <div>
                <img :src="value['data']['details']['image']" alt="A Background Image">    
            </div>
            <div>
                <div>
                    <span>{{ value['data']['details']['rating'] }} ({{ value['data']['details']['review'] }} reviews)</span><span class="text-xs">{{ value['data']['details']['star'] }}</span>
                    <h1 class="text-2xl font-semibold">{{ value['data']['details']['name'] }}</h1>
                    <p>{{ value['data']['details']['location'] }}</p>
                    <p>{{ value['data']['details']['state'] }}</p>
                    <p>{{ value['data']['details']['country'] }}</p>
                    <p>$200 <span class="text-sm">Per Night</span></p>
                    <NuxtLink :to="'/book/hotel/' + slugify(value['data']['details']['name'])" class="bg-black text-white px-6 py-2 my-5 text-semibold rounded-md inline-block">
                        Book
                    </NuxtLink>
                </div>
                RecordID: {{ value['id'] }} <br>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'


const { $web5: web5, $myDID: myDID } = useNuxtApp();
const hotels = ref([])

const getRecords = async() => {
    try {
        const { records } = await web5.dwn.records.query({
            from: "did:ion:EiARjrMGhKrU4t0qmF091DhriLVNK9EcozAZLbxmzRxbsA:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJkd24tc2lnIiwicHVibGljS2V5SndrIjp7ImNydiI6IkVkMjU1MTkiLCJrdHkiOiJPS1AiLCJ4IjoiRUhfWUUwRG0tWEtONlN0NkxDM0JoXzNUVXQ1Y0w1eXVnSXA0LWEwNUFhUSJ9LCJwdXJwb3NlcyI6WyJhdXRoZW50aWNhdGlvbiJdLCJ0eXBlIjoiSnNvbldlYktleTIwMjAifSx7ImlkIjoiZHduLWVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJEeHVZSkNtWEw4RE53M18wVXRMS0RjSzlTekNJcWZEMTRUZTlnaW1JM2NBIiwieSI6IjdqSTFuZ2o4UzBnaGhKWUZnUWN5aTFoeXBNbXhORXl1Umc5TS1HYnFMZVEifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7ImVuY3J5cHRpb25LZXlzIjpbIiNkd24tZW5jIl0sIm5vZGVzIjpbImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduNiIsImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduNCJdLCJzaWduaW5nS2V5cyI6WyIjZHduLXNpZyJdfSwidHlwZSI6IkRlY2VudHJhbGl6ZWRXZWJOb2RlIn1dfX1dLCJ1cGRhdGVDb21taXRtZW50IjoiRWlDVWxUNFZPV3RHMDJZdlZ6dHZEd1dIN2tQdHdiM3ZpLWktSWpLOFBYd1k0ZyJ9LCJzdWZmaXhEYXRhIjp7ImRlbHRhSGFzaCI6IkVpQ21MczZzTGgxRGRXU09CRFJuOVUxSEhxQzlRZG9NOExiM1BXZU1ibDBod1EiLCJyZWNvdmVyeUNvbW1pdG1lbnQiOiJFaUNHVHdZRzNGdlVTZ0lSS2YzOWtUZ0prVkRHYUFubzBUVUNkNm9vVWVSSC1nIn19",
            message: {
                filter: {
                    protocol: hotelReservationProtocol.protocol,
                    protocolPath: "hotelDetails",
                    dataFormat: hotelReservationProtocol.types.hotelDetails.dataFormats[0],
                    schema: hotelReservationProtocol.types.hotelDetails.schema,
                },
            }
        });

        for (let record of records) {
            const data = await record.data.json();
            const list = { data, id: record.id};
            hotels.value.push(list)
            console.log("hello", list)
        }
    } catch (e) {
        console.error(e)
        return
    }
}

async function search()
{
    const configureProtocol = async () => {
        // query the list of existing protocols on the DWN
        const { protocols, status } = await web5.dwn.protocols.query({
            message: {
                filter: {
                    protocol: hotelReservationProtocol.protocol,
                }
            }
        });

        if(status.code !== 200) {
            alert('Error querying protocols');
            console.error('Error querying protocols', status);
            return;
        }

        // if the protocol already exists, we return
        if(protocols.length > 0) {
            console.log('Protocol already exists');
            return;
        }

        // configure protocol on local DWN
        const { status: configureStatus, protocol } = await web5.dwn.protocols.configure({
            message: {
                definition: hotelReservationProtocol,
            }
        });

        protocol.send(myDID)

        console.log('Protocol configured', configureStatus, protocol);
    }

    await configureProtocol()
    await getRecords()
}

if(hotels.value)
{

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
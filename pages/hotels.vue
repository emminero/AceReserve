<template>
    <div>
        <div class="w-1/2 my-10 m-auto flex justify-center h-[300px]">
            <div class="flex flex-col w-full">
                <textarea class="border border-gray-500 mt-10 w-full h-full p-2" placeholder="Input your DID" v-model="text"></textarea>
                <button @click="search" class="px-4 py-2 bg-purple-600 mt-2">Check Rooms</button>
                <button @click="createEmptyRoom" class="px-4 py-2 bg-purple-600 mt-2">Create Empty Rooms Records to my DWN</button>
            </div>
        </div>
    </div>

    <div>
        {{ response }}
    </div>
</template>

<script setup>
import { ref } from 'vue';
import emptyRooms from '~/assets/Rooms/empty-rooms.json'
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'

const { $web5: web5, $myDID: myDID } = useNuxtApp();
const text = ref('')
const response = ref([])

//Send Personal Data to DWN 
const sendEmptyRoom = async() => {
    try{
        const { record }  = await web5.dwn.records.create({
            data: emptyRooms,
            message: {
                protocol: hotelReservationProtocol.protocol,
                protocolPath: 'emptyRooms',
                published: true,
                dataFormat: hotelReservationProtocol.types.emptyRooms.dataFormats[0],
                schema: hotelReservationProtocol.types.emptyRooms.schema,
            }
        });

        const result = await record.data.json()
        const message = {
            record, result, id: record.id
        }

        const { status: sendStatus } = await record.send(myDID);

        if (sendStatus.code !== 202) {
            console.log("Unable to send to target did:" + sendStatus);
            return;
        }
        else {
            console.log("Empty room details sent to recipient");
        }

        //https://developer.tbd.website/docs/web5/build/decentralized-web-nodes/send-to-dwn

        console.log("message:", message)
    } catch (e) {
        console.error(e);
        return;
    }
}


async function createEmptyRoom()
{
    await sendEmptyRoom()
    console.log('hello')
}

// onBeforeMount(async () => {

//     // Fetch shared todo lists
//     const{ records } = await web5.dwn.records.query({
//         message: {
//             filter: {
//                 schema: hotelReservationProtocol.types.emptyRooms.schema
//             },
//             dateSort: 'createdAscending'
//         }
//     });

//     console.log("Saved records", records);
// });

const getRecords = async() => {
    try {
        const { records } = await web5.dwn.records.query({
            message: {
                filter: {
                    protocol: hotelReservationProtocol.protocol,
                    protocolPath: "emptyRooms",
                    dataFormat: hotelReservationProtocol.types.emptyRooms.dataFormats[0],
                    schema: hotelReservationProtocol.types.emptyRooms.schema,
                },
            }
        });

        for (let record of records) {
            const data = await record.data.json();
            const list = {record, data, id: record.id};

            console.log("hello", list)
        }
        // console.log('hey')
        // const response = await web5.dwn.records.query({
        //     message: {
        //         filter: {
        //             schema: hotelReservationProtocol.types.emptyRooms.schema,
        //             },
        //         },
        //     });

        //     // Loop through returned records and print text from each
        //     response.records.forEach(async record => {
        //         console.log(await record.data.text());
        //     });
    } catch (e) {
        console.error(e)
        return
    }
}

async function search()
{
    await getRecords()
}
</script>
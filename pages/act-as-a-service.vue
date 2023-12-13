<template>
    <div class="w-4/5 mx-auto flex justify-center items-center py-10">
        <div class="w-full md:w-1/2 flex flex-col justify-center p-4 h-[500px]">
            <textarea v-model="myDID" class="border border-black rounded-sm mt-2 w-full h-3/5 p-2 block" placeholder="Input your DID"></textarea>
            <p class="text-md text-center font-semibold text-red-600">{{ error }}</p>
            <p class="text-sm mt-2">Click to get a demo record ID</p>
            <button @click="getRecord" class="bg-black text-white mt-2 inline py-2 ">Get Record Id</button>

            <hr class="border mt-10">

            <div v-show="active" class="mt-10 flex flex-col border-4 py-2">
                <p class="text-sm text-center mt-1">We have installed a protocol to your project and have download some data to your DWN</p>
                <button @click="copyRecord()" class="bg-black text-white mt-2 w-1/2 py-2 mx-auto">Copy your Record ID</button>
                <NuxtLink to="/register" class="text-sm underline text-blue-600 text-center block">Proceed to the register page to regiser with your recordID</NuxtLink>
            </div>
        </div>
    </div>
</template>

<script setup>
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'

const { $web5: web5, $myDID: myDID } = useNuxtApp();
const error = ref('')
const messages = ref([])
const active = ref(false)
const recordId = ref('')

const copyRecord = async() => {
    await navigator.clipboard.writeText(recordId.value);
    alert('RecordId copied to clipboard');
}


async function getRecord(){
    if(myDID) {
        //Installing Protocol

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
                alert('Hotel protocol already exist but successfully registered to our application.')
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
            alert('Successful registered and Hotel protocol successfully installed.')
        }

        await configureProtocol()

        // Install Data to the service DWN
        function random(arr) {
            const element = arr[(Math.floor(Math.random() * arr.length))];
            return element
        }
        const images = [
            "https://images.unsplash.com/photo-1611892440504-42a792e24d32?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8aG90ZWwlMjByb29tfGVufDB8fDB8fHww",
            "https://images.unsplash.com/photo-1568495248636-6432b97bd949?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fGhvdGVsJTIwcm9vbXxlbnwwfHwwfHx8MA%3D%3D",
            "https://images.unsplash.com/photo-1578774204375-826dc5d996ed?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OTR8fGhvdGVsfGVufDB8fDB8fHww",
            "https://images.unsplash.com/photo-1566665797739-1674de7a421a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTl8fGhvdGVsJTIwcm9vbXxlbnwwfHwwfHx8MA%3D%3D",
            "https://media.istockphoto.com/id/1304826235/photo/luxury-bathroom-interior-with-shower-toilet-mirror-and-yellow-towels.jpg?s=612x612&w=0&k=20&c=bUEbM3oGL_28QbeXrozy1ITjYFME42D2uOGrYh8iOkI=",
            "https://media.istockphoto.com/id/1309074908/photo/luxury-bathroom-interior-with-hot-tub-and-beautiful-sea-view.jpg?s=612x612&w=0&k=20&c=yXIL9RMkdWthXsvCddeNexVxBCj16UNHBgckCTxF4PA="
        ]

        
        const price = [3000, 4000, 8000, 7000, 8000, 9000]

        const cancellation = ['Full Flexible', 'Flexible', 'No Resembolsable']

        const rooms = [
            "Single", "Double", "Twin", "King Size", "Queen Size", "Suite", "Presidential"
        ]

        const value = [true, false]

        const hotelDetail = {
            "@type" : "hotelDetails",
            "details" : {
                "name" : 'Manual Hotel and Suite',
                "email": "support@hotel.com",
                "location": "No 8b Manual Address",
                "did": myDID,
                "type": "hotel",
                "star": 3,
                "state": "Lagos",
                "country": "Nigeria",
                "image": "https://images.unsplash.com/photo-1568084680786-a84f91d1153c?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mjd8fGhvdGVsfGVufDB8fDB8fHww",
                "rating": "9/10",
                "review": "436",
                "images": images,
                "cancellation": random(cancellation),
                "roomTypes" : [
                    {
                        "type": random(rooms),
                        "price": random(price),
                        "availability": random(value)
                    },
                    {
                        "type": random(rooms),
                        "price": random(price),
                        "availability": random(value)
                    },
                    {
                        "type": random(rooms),
                        "price": random(price),
                        "availability": random(value)
                    }
                ],
                "breakfast": random(value),
                "freeWifi": random(value),
                "parkingLot": random(value),
                "reception": random(value),
                "swimmingPool": random(value)
            }
        }

        const sendHotelDetail = async() => {
            try{
                const { record }  = await web5.dwn.records.create({
                    data: hotelDetail,
                    message: {
                        protocol: hotelReservationProtocol.protocol,
                        protocolPath: 'hotelDetails',
                        published: true,
                        dataFormat: hotelReservationProtocol.types.hotelDetails.dataFormats[0],
                        schema: hotelReservationProtocol.types.hotelDetails.schema,
                    }
                });

                const result = await record.data.json()
                const message = {
                    record, result, id: record.id
                }
                messages.value.push(message)

                // Sending the created information to myDID
                const { status: sendStatus } = await record.send(myDID);

                if (sendStatus.code !== 202) {
                    console.log("Unable to send to target did:" + sendStatus);
                    return;
                }
                else {
                    console.log("Hotel details sent to recipient DWN");
                }

                console.log("message:", message)
            } catch (e) {
                console.error(e);
                return;
            }
        }
        
        await sendHotelDetail()
        active.value = true

    }else {
        error.value = "Input your DID"
    }
    messages.value.forEach(element => {
        recordId.value = element.id        
    });

}
</script>
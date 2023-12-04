<template>
    <div>
        <div class="w-1/2 m-auto flex justify-center h-[600px]">
            <div class="flex flex-col w-full">
                <h1>Welcome, Team Ace</h1>
                <button @click="showDID" class="px-4 py-2 bg-purple-600">Show my DID</button>
                <textarea class="border border-gray-500 mt-10 w-full h-full p-2" v-model="text"></textarea>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'
    const { $web5: web5, $myDID: myDID } = useNuxtApp();
    const text = ref('')

        function showDID(){
            text.value = myDID
        }
    // console.log(myDID);

    //Installing a protocol to my DWN and anybodies DWN.
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

    onBeforeMount(async () => {
        await configureProtocol()
    })

    //I want to send list of booked rooms to my DWN to be queried by anybody.
    
</script>
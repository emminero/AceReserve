<template>
    <div>
        <!-- <div class="w-1/2 m-auto flex justify-center h-[600px]">
            <div class="flex flex-col w-full">
                <h1 class="text-bold text-4xl">Welcome, Team Ace</h1>
                <p>The site is under construction...</p> -->
                <!-- <button @click="showDID" class="px-4 py-2 bg-purple-600">Show my DID</button>
                <textarea class="border border-gray-500 mt-10 w-full h-full p-2" v-model="text"></textarea> -->

                <!-- <div class="w-1/2 mx-auto mt-10"> -->
                    <!-- <div class="py-10">
                        <h1 class="pb-5">Register as a service provider</h1>
                        <NuxtLink to="register" class="bg-black text-white px-4 py-2 text-semibold rounded-md">
                            Register
                        </NuxtLink>
                    </div>
                </div>
            </div>
        </div> -->
        <main>
            <section class="border">
                <div>

                </div>
            </section>

            <section class="relative">
                <div class="absolute inset-0 bg-black opacity-70 z-30"></div>
                <div class="w-5/6 mx-auto py-16 relative z-40">
                    <div class="w-4/5">
                        <h1 class="text-[58px] font-bold text-white">Spend your time in your dream places, we fly the best</h1>
                        <div class="w-4/5">
                            <p class="my-10 font-medium text-white">
                                Lorem ipsum dolor sit amet consectetur. Interdum vulputate fermentum odio vitae nibh nulla ornare consequat. Bibendum vel ac egestas quis venenatis. Aliquam ac cras tristique risus eros eget. Tortor felis placerat sit lobortis. Mattis mattis ornare mattis suspendisse nunc dolor. Neque magna auctor nulla gravida. Elit scelerisque at dui et condimentum tortor eu sagittis. Mauris venenatis mauris ipsum consectetur egestas magna viverra eu donec. Nisi vulputate id feugiat nec. Velit volutpat.
                            </p>
                        </div>
                        <div>
                            <button class="p-4 border text-white">Read More</button>
                        </div>
                    </div>
                </div>
            </section>
        </main>
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

    // onBeforeMount(async () => {
    //     await configureProtocol()
    // })

    //I want to send list of booked rooms to my DWN to be queried by anybody.
    
</script>
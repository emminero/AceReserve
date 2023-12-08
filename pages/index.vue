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
            <section class="relative">
                <div class="absolute inset-0 bg-black opacity-70 z-30"></div>
                <div class="w-5/6 mx-auto py-16 relative z-40">
                    <div class="w-4/5">
                        <h1 class="text-[58px] font-bold text-white">Spend your time in your dream places, we fly the best</h1>
                        <div class="w-4/5">
                            <p class="my-10 font-medium text-white tracking-widest">
                                Lorem ipsum dolor sit amet consectetur. Interdum vulputate fermentum odio vitae nibh nulla ornare consequat. Bibendum vel ac egestas quis venenatis. Aliquam ac cras tristique risus eros eget. Tortor felis placerat sit lobortis. Mattis mattis ornare mattis suspendisse nunc dolor. Neque magna auctor nulla gravida. Elit scelerisque at dui et condimentum tortor eu sagittis. Mauris venenatis mauris ipsum consectetur egestas magna viverra eu donec. Nisi vulputate id feugiat nec. Velit volutpat.
                            </p>
                        </div>
                        <div>
                            <button class="p-4 border text-white">Read More</button>
                        </div>
                    </div>
                </div>
            </section>

            <section>
                <div class="w-5/6 mx-auto py-16">
                    <h1 class="mb-10 text-[23px] font-medium">About Us</h1>
                    <div class="flex justify-between">
                        <div class="w-1/2">
                            <h1 class="text-[58px] leading-normal font-bold text-[#000]">
                                We Are Here To Make Your Feeling Look More Elegant
                            </h1>
                            <p class="my-8">Lorem ipsum dolor sit amet consectetur. Orci eleifend ac gravida eleifend. Dignissim suspendisse aliquam velit id risus consequat. Viverra ridiculus bibendum urna metus ornare. Odio commodo amet eu ornare id proin proin proin. Eleifend viverra tellus cras vitae faucibus elit nunc hac. In platea eget et scelerisque. Quis in gravida habitasse tortor pretium ac non faucibus et. Id sit condimentum consectetur venenatis pretium. Egestas quis tellus pellentesque consequat nulla aliquam odio et. Scelerisque neque in ut sed in. Lectus egestas lorem vitae tellus dignissim eget. Sed diam semper sit enim leo pellentesque sollicitudin cursus.</p>

                            <p class="my-8">Malesuada fermentum enim tellus id arcu arcu. Lacus aliquet donec duis habitasse. Nisl arcu libero elit commodo duis quam. Et placerat suscipit turpis ullamcorper sed. Imperdiet quis id mattis pharetra et massa donec. Lectus suscipit nibh orci morbi lectus egestas. Eu cras feugiat bibendum in nisl molestie elit id ut. Ipsum senectus quam orci velit..</p>
                            <div>
                                <button class="bg-[#121201] rounded-[20px] px-6 py-3 font-medium text-sm text-white box">
                                    Get your Reservation
                                </button>
                            </div>
                        </div>
                        <div class="w-1/2 h-1/2 pl-4 grid">
                            <div class="grid-area">
                                <img class="object-fit w-full h-fit" src="~/assets/images/about-us.jpg" alt="About Us Image">
                            </div>
                            <div class="grid-area items-end -mb-56 justify-end grid -mr-16">
                                <img class="object-fit w-full h-fit" src="~/assets/images/about-us(1).jpg" alt="About Us Image">
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <section>
                <div class="w-5/6 mx-auto py-16">
                    <h1 class="text-[56px] font-bold text-center">A Place like home with excessive comfort</h1>

                    <div class="grid grid-cols-3 gap-x-10 justify-between my-10">
                        <div>
                            <div class="h-1/2">
                                <img class="object-fit w-full h-full" src="~/assets/images/room.jpg" alt="About Us Image">
                            </div>

                            <div>
                                <span class="text-[23px] font-medium my-5 block">Room & lounge</span>
                            </div>

                            <div class="pr-2">
                                <p>
                                    Lorem ipsum dolor sit amet consectetur. Ultricies vitae nec non fames volutpat arcu ut. At adipiscing mattis sit ac amet vulputate eu congue ultrices. Donec diam purus etiam 
                                </p>
                            </div>

                            <div>
                                <button class="py-3 px-6 bg-[#121201] box mt-8 text-white rounded-[20px] font-medium">
                                    Book Now
                                </button>
                            </div>
                        </div>

                        <div>
                            <div class="h-1/2">
                                <img class="object-fit w-full h-full" src="~/assets/images/bedroom.jpg" alt="About Us Image">
                            </div>

                            <div>
                                <span class="text-[23px] font-medium my-5 block">Bedroom only</span>
                            </div>

                            <div class="pr-2">
                                <p>
                                    Lorem ipsum dolor sit amet consectetur. Ultricies vitae nec non fames volutpat arcu ut. At adipiscing mattis sit ac amet vulputate eu congue ultrices. Donec diam purus etiam 
                                </p>
                            </div>

                            <div>
                                <button class="py-3 px-6 bg-[#121201] box mt-8 text-white rounded-[20px] font-medium">
                                    Book Now
                                </button>
                            </div>
                        </div>

                        <div>
                            <div class='h-1/2'>
                                <img class="object-fit w-full h-full" src="~/assets/images/dinner.jpg" alt="About Us Image">
                            </div>

                            <div>
                                <span class="text-[23px] font-medium my-5 block">Dinner only</span>
                            </div>

                            <div class="pr-2">
                                <p>
                                    Lorem ipsum dolor sit amet consectetur. Ultricies vitae nec non fames volutpat arcu ut. At adipiscing mattis sit ac amet vulputate eu congue ultrices. Donec diam purus etiam 
                                </p>
                            </div>

                            <div>
                                <button class="py-3 px-6 bg-[#121201] box mt-8 text-white rounded-[20px] font-medium">
                                    Book Now
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <section class="bg-[#121201]">
                <div class="w-5/6 mx-auto py-16">
                    <div class="flex py-10 justify-between gap-x-3">
                        <div class="w-2/5">
                            <h1 class="text-5xl text-white font-medium leading-[70.5px]">Let ride you and your luggages</h1>
                            <p class="tracking-wider mt-10 mb-5 text-white leading-[21px]">
                                At Ace Reserve, we understand that the journey is just as important as the destination. That's why our luxury car rental service is meticulously designed to add a touch of sophistication to your travels. Embark on a road trip of a lifetime with our diverse and meticulously maintained fleet of luxury vehicles. From sleek sports cars to spacious SUVs, we offer a range of options to suit your preferences and needs.
                            </p>
                            <div>
                                <button class="p-4 border text-white">Read More</button>
                            </div>
                            <div class="pt-20">
                                <button class="bg-white rounded-[30px] w-3/5 py-4 text-[#121201] font-semibold text-xl">Hire us</button>
                            </div>
                        </div>

                        <div class="w-3/5 h-[550px]">
                            <div class="flex justify-between gap-x-10">
                                <div>
                                    <img class="object-fit w-full h-fit" src="~/assets/images/car-1.jpg" alt="AceReserve Services">
                                </div>
                                <div>
                                    <img class="object-fit w-full h-fit" src="~/assets/images/car-2.jpg" alt="AceReserve Services">
                                </div>
                            </div>
                           <div class="grid">
                                <div class="flex justify-end -mt-10 mr-10">
                                    <img class="object-fit w-[450px] h-fit" src="~/assets/images/car-3.jpg" alt="AceReserve Services">
                                </div>
                           </div>
                        </div>
                    </div>
                </div>
            </section>

            <section class="relative">
                <div class="py-16 mx-auto w-5/6">
                    <div class="bg-black inset-0 absolute"></div>
                    <div class="w-4/5 relative z-40">
                        <h1 class="text-[58px] text-white leading-[87px] font-semibold">Take flight with us and enjoy our lifetime partnership</h1>
                        <p class="my-8 pr-4 text-white text-2xl">Unleash your wanderlust with Ace Reserve's intuitive flight booking system. Discover a world of destinations at your fingertips and embark on your dream journey stress-free.</p>
                        <button class="px-8 mt-4 font-medium text-xl bg-white rounded-[30px] py-4">Book now</button>
                    </div>
                </div>
            </section>

            <section>
                <div class="py-16 w-5/6 mx-auto">
                    <h1 class="text-[47px] font-semibold">Domestic and International Flight 24/7</h1>
                    <div class="flex justify-between my-10">
                        <div class="w-1/2 pr-8 py-2">
                            <h1 class="text-2xl font-semibold">Discover a World of Destinations</h1>
                            <p class="my-8">Navigate through a curated selection of destinations that span the globe. From exotic getaways to bustling metropolises, our platform opens the door to a world of possibilities.</p>
                            <h1 class="text-2xl font-semibold">Travel Experience Tailored to Your Tastes</h1>
                            <p class="my-8">Customize your travel experience with ease. Whether you're seeking cultural immersion, scenic landscapes, or vibrant city life, Ace Reserve allows you to tailor your journey to match your unique preferences.</p>
                            <button class="p-4 border border-[#121201] text-[#121201]">Read More</button>
                        </div>
                        <div class="h-[450px]">
                            <img class="object-fit w-full h-full" src="~/assets/images/flight.jpg" alt="AceReserve Flight Services">
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

<style scoped>
.box {
    box-shadow: 0px 8px 30px 6px rgba(0, 0, 0, 0.16), 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
}
.grid-area {
    grid-area: 1 / -1;
}
</style>
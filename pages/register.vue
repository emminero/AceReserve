<template>
    <div class="w-4/5 mx-auto flex justify-center items-center py-10">
        <div class="w-full md:w-1/2 flex flex-col justify-center p-4 h-[500px]">
            <select v-model="services" name="services" id="services" class="bg-black text-white px-4 py-2 rounded-md">
                <option value="" disabled>Select an option</option>
                <option value="hotel">Hotel Reservation</option>
                <option value="car">Car Rental</option>
                <option value="flight">Flight Reservation</option>
                <option value="ticket">Ticket</option>
            </select>

            <textarea v-model="userDID" class="border border-black rounded-sm mt-2 w-full h-3/5 p-2 block" placeholder="Input your DID"></textarea>
            <p class="text-md text-center font-semibold text-red-600">{{ error }}</p>
            <button @click="register" class="bg-black text-white mt-2 inline py-2 ">Register</button>

            <hr class="border mt-10">
            <div class="flex flex-col">
                <p class="text-sm text-center mt-1">For the purpose of this project, you can act as a service provider.</p>
                <button v-show="myDID" @click="copyDID()" class="bg-black text-white mt-2 w-3/5 py-2 mx-auto">Copy your generated DID</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'


const { $web5: web5, $myDID: myDID } = useNuxtApp();
const services = ref('')
const error = ref('')
const userDID = ref('')

const copyDID = async() => {
    await navigator.clipboard.writeText(myDID);
    alert('DID copied to clipboard');
}

function isEmpty(string) {
  return typeof string === 'string' && string.length === 0;
}

const register = async() => {
    if(isEmpty(services.value)) return error.value = "Select a service"
    else if(isEmpty(userDID.value)) return error.value = "Input your DID"

    if(services.value == 'hotel'){
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
                alert('Hotel protocol already exist and successfully registered.')
                return;
            }

            // configure protocol on local DWN
            const { status: configureStatus, protocol } = await web5.dwn.protocols.configure({
                message: {
                    definition: hotelReservationProtocol,
                }
            });

            if(userDID.value != myDID){
                protocol.send(userDID)
            }
            protocol.send(myDID)

            console.log('Protocol configured', configureStatus, protocol);
            alert('Successful registered and Hotel protocol successfully installed.')
        }

        await configureProtocol()
    }

    //Create Hotel Details

    const hotelDetails = {
        "@type" : "hotelDetails",
        "details" : {
            "name" : "Golden Villa Suite",
            "location": "James Street, Lagos",
            "star": "3 stars",
            "state": "Lagos",
            "country": "Nigeria"
        }
    }

    console.log(hotelDetails)

    try{
        const { record }  = await web5.dwn.records.create({
            data: hotelDetails,
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

        const { status: sendStatus } = await record.send(myDID);

        if (sendStatus.code !== 202) {
            console.log("Unable to send to target did:" + sendStatus);
            return;
        }
        else {
            console.log("Hotel details sent to recipient");
        }

        //https://developer.tbd.website/docs/web5/build/decentralized-web-nodes/send-to-dwn

        console.log("message:", message)
    } catch (e) {
        console.error(e);
        return;
    }

    // await navigateTo('/hotel')
}
</script>
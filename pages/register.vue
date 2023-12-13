<template>
    <div class="w-4/5 mx-auto flex justify-center items-center py-10">
        <div class="w-full md:w-1/2 flex flex-col justify-center p-4 h-[500px]">
            <select v-model="services" name="services" id="services" class="bg-black text-white px-4 py-2 rounded-md">
                <option value="" disabled>Select an option</option>
                <option value="hotel">Hotel Reservation</option>
                <option value="flight">Flight Reservation</option>
            </select>

            <input type="text" v-model="userRecordId" class="border border-black rounded-sm mt-2 w-full p-2 block" placeholder="Input record ID of your hotel details" required>
            <p class="text-md text-center font-semibold text-red-600">{{ error }}</p>
            <button @click="register" class="bg-black text-white mt-2 inline py-2 ">Register</button>

            <hr class="border mt-10">
            <div class="flex flex-col">
                <p class="text-sm text-center mt-1">For the purpose of this project, you can act as a service provider. Wait for few seconds for your did to generate</p>
                <p v-show="!myDID" class="text-green-600 text-center font-bold">Generating/getting your DID....</p>
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
const userRecordId = ref('')
const companyDID = ref('')

const copyDID = async() => {
    await navigator.clipboard.writeText(myDID);
    alert('DID copied to clipboard');
}

function isEmpty(string) {
  return typeof string === 'string' && string.length === 0;
}

companyDID.value = "did:ion:EiDJbML7UODRf_T_gjJJxiHSo1K9HY5FBSk3tWWU8z9rdg:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJkd24tc2lnIiwicHVibGljS2V5SndrIjp7ImNydiI6IkVkMjU1MTkiLCJrdHkiOiJPS1AiLCJ4IjoiYXhSTFVTZ25SeVJjX3VhWWs5RTFHWlNIZmItSVhsQUhjTlpEOXFSeE1POCJ9LCJwdXJwb3NlcyI6WyJhdXRoZW50aWNhdGlvbiJdLCJ0eXBlIjoiSnNvbldlYktleTIwMjAifSx7ImlkIjoiZHduLWVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJIQ1Y0Rmx2c0l1OUZXRy1hSnQ2cDlSRm9LV19kX3BNN1N6cXR2c25iZWFjIiwieSI6ImQ5aExqbVRfdDlBSTRpUkhibEFTRG5jWkZBYTYzcjFRN0JKRklsdFkycTQifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7ImVuY3J5cHRpb25LZXlzIjpbIiNkd24tZW5jIl0sIm5vZGVzIjpbImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduMSIsImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduMiJdLCJzaWduaW5nS2V5cyI6WyIjZHduLXNpZyJdfSwidHlwZSI6IkRlY2VudHJhbGl6ZWRXZWJOb2RlIn1dfX1dLCJ1cGRhdGVDb21taXRtZW50IjoiRWlCRkFKb2ktdEcwUVRuNWtnbFpIQ25rNFJJWnc1NWd1RThoM0RkVnZrbk8zdyJ9LCJzdWZmaXhEYXRhIjp7ImRlbHRhSGFzaCI6IkVpRGZ0dndrakU5dlN0bTF2WkNnSV96SDNKNFYydVdiYVNMcDVrclk1YmFkelEiLCJyZWNvdmVyeUNvbW1pdG1lbnQiOiJFaUJfVFRVSFdpVVI4TXBwV2FBaEFsNmZFLXZTM2VPTXhDdVhOOE1tMGt3SjBRIn19"

const register = async() => {
    if(isEmpty(services.value)) return error.value = "Select a service"

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
                return;
            }

            // configure protocol on local DWN
            const { status: configureStatus, protocol } = await web5.dwn.protocols.configure({
                message: {
                    definition: hotelReservationProtocol,
                }
            });

            protocol.send(userDID)

            console.log('Protocol configured', configureStatus, protocol);
        }

        await configureProtocol()

        const getAndSendRecord = async() => {
            console.log(userRecordId.value)
            try{
                // Reads the indicated record from the user's DWNs
                let { record } = await web5.dwn.records.read({
                    message: {
                        filter: {
                            recordId: userRecordId.value,
                        },
                    },
                });

                // console.log(await record.data.json())
                // Sending the created information to myDID
                const { status: sendStatus } = await record.send(companyDID.value);

                if (sendStatus.code !== 202) {
                    console.log("Unable to send to target did:" + JSON.stringify(sendStatus));
                    return;
                }
                else {
                    console.log("Record details sent to Companies DWN");
                }
            } catch (e) {
                console.error(e);
                return;
            }
        }
        
        await getAndSendRecord()

    }
}

//Create Hotel Details


</script>
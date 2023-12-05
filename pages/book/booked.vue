<template>
    <div>
        <h1 class="text-center mt-5 mb-10 font-semibold text-2xl">Empty Rooms</h1>
        <div class="w-4/5 flex justify-center mx-auto">
            <div class="grid grid-cols-3 gap-10" v-for="rooms in emptyRooms">
                <div v-for="room in rooms['emptyRooms']">
                    <div>
                        <img :src="room['image']" alt="Room Image">
                        <p>Room: {{ room['roomNo'] }}</p>
                        <button class="bg-black text-white px-6 py-2 my-5 text-semibold rounded-md inline-block">Book</button>
                    </div>
                </div>
            </div>
        </div>


        <button @click="vc()" class="bg-black text-white px-6 py-2 my-5 text-semibold rounded-md inline-block">Get VC for a room</button>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { VerifiableCredential } from '@web5/credentials';
import { DidDht, DidKeyMethod } from '@web5/dids';
import { Ed25519 } from '@web5/crypto';
import hotelReservationProtocol from '~/assets/sharedProtocols/hotel-reservation-protocol.json'

const { $web5: web5, $myDID: myDID } = useNuxtApp();

const empty = ref([])

const emptyRooms = ref([])

const getEmptyRoom = async() => {
    try {
        const { records } = await web5.dwn.records.query({
            from: "did:ion:EiARjrMGhKrU4t0qmF091DhriLVNK9EcozAZLbxmzRxbsA:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJkd24tc2lnIiwicHVibGljS2V5SndrIjp7ImNydiI6IkVkMjU1MTkiLCJrdHkiOiJPS1AiLCJ4IjoiRUhfWUUwRG0tWEtONlN0NkxDM0JoXzNUVXQ1Y0w1eXVnSXA0LWEwNUFhUSJ9LCJwdXJwb3NlcyI6WyJhdXRoZW50aWNhdGlvbiJdLCJ0eXBlIjoiSnNvbldlYktleTIwMjAifSx7ImlkIjoiZHduLWVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJEeHVZSkNtWEw4RE53M18wVXRMS0RjSzlTekNJcWZEMTRUZTlnaW1JM2NBIiwieSI6IjdqSTFuZ2o4UzBnaGhKWUZnUWN5aTFoeXBNbXhORXl1Umc5TS1HYnFMZVEifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7ImVuY3J5cHRpb25LZXlzIjpbIiNkd24tZW5jIl0sIm5vZGVzIjpbImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduNiIsImh0dHBzOi8vZHduLnRiZGRldi5vcmcvZHduNCJdLCJzaWduaW5nS2V5cyI6WyIjZHduLXNpZyJdfSwidHlwZSI6IkRlY2VudHJhbGl6ZWRXZWJOb2RlIn1dfX1dLCJ1cGRhdGVDb21taXRtZW50IjoiRWlDVWxUNFZPV3RHMDJZdlZ6dHZEd1dIN2tQdHdiM3ZpLWktSWpLOFBYd1k0ZyJ9LCJzdWZmaXhEYXRhIjp7ImRlbHRhSGFzaCI6IkVpQ21MczZzTGgxRGRXU09CRFJuOVUxSEhxQzlRZG9NOExiM1BXZU1ibDBod1EiLCJyZWNvdmVyeUNvbW1pdG1lbnQiOiJFaUNHVHdZRzNGdlVTZ0lSS2YzOWtUZ0prVkRHYUFubzBUVUNkNm9vVWVSSC1nIn19",
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
            const list = { data, id: record.id};
            empty.value.push(list)
            console.log("hello", list)
        }

        console.log(empty.value[1]['data']['name'])
        emptyRooms.value = empty.value[1]
    } catch (e) {
        console.error(e)
        return
    }
}

// onBeforeMount(async () => {
//         await getEmptyRoom()
//     })

    async function vc() {
        const issuerDID = await DidKeyMethod.create()
        const subjectDID = await DidKeyMethod.create()

        let currentDate = new Date().toJSON().slice(0, 10);

        function addDays(date, days) {
            var result = new Date(date);
            result.setDate(result.getDate() + days);
            return result;
        }

        class BookedRoom{
            constructor(detail, date) {
                this.detail = detail
                this.date = date
            }
       }
        
        //type, issuer, subject, data
        const vc = VerifiableCredential.create({
            type: 'bookedRooms',
            issuer: issuerDID.did,
            subject: subjectDID.did,
            data: new BookedRoom('booked Room 4', currentDate)
        })

        const privateKey = issuerDID.keySet.verificationMethodKeys[0].privateKeyJwk

        const signOptions = {
            issuerDid: issuerDID.did,
            subject: subjectDID.did,
            kid: `${issuerDID.did}#${issuerDID.did.split(':')[2]}`,
            signer: async (data) => await Ed25519.sign({ data, key: privateKey })            
        }
        
        const vcJwt = await vc.sign(signOptions)

        console.log(vcJwt)

        try {
            await VerifiableCredential.verify(vcJwt)
            console.log("VC Verification successful!")
        } catch (e) {
            console.log("VC Verification failed: ${e.message}")
        }

        const parseVc = VerifiableCredential.parseJwt(vcJwt)

        // console.log('\nParsed VC: \n' + parseVc.toString() + '\n')

        const { record }  = await web5.dwn.records.create({
            data: vcJwt,
            message: {
                dataFormat: 'application/vc+jwt',
                schema: 'bookedRooms',
            }
        })

        console.log('Record ID', record.id)

        let { record: readRecord } = await web5.dwn.records.read({
            message: {
                filter: {
                    recordId: record.id
                }
            }
        })

        const readVcJwt = await readRecord.data.text();
        // console.log(readVcJwt)
    }
</script>
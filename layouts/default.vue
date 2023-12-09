<template>
    <div>
        <Head>
            <Title>AceReserve - A decentralized All-in-Booking Application</Title>
            <Meta name="description" content="A web5 decentralized all-in-one booking application" /> 
        </Head>
        <header>
            <div class="w-11/12 mx-auto py-8 flex justify-between items-center">
                <div>
                    <NuxtLink to="/">
                        <p>AceReserve</p>
                    </NuxtLink>
                </div>
                <div class="flex justify-between w-1/2 items-center">
                    <nav>
                        <ul class="flex space-x-10 items-center">
                            <li>
                                <NuxtLink>
                                    Flight
                                </NuxtLink>
                            </li>
                            <li>
                                <NuxtLink to="/hotel/">
                                    Hotels
                                </NuxtLink>
                            </li>
                            <li>
                                <NuxtLink>
                                    Car Hiring
                                </NuxtLink>
                            </li>
                            <li>
                                <NuxtLink>
                                    E-Ticket
                                </NuxtLink>
                            </li>
                        </ul>
                    </nav>
                    <div>
                        <NuxtLink to="register" class="bg-black text-white rounded-md px-6 py-2">
                            Register
                        </NuxtLink>
                    </div>
                </div>
            </div>
        </header>

        <slot />
    </div>
</template>

<script setup>

</script>
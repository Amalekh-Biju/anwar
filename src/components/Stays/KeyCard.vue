<template>
    <div class="overflow-hidden border-[0.5px]  border-gray-400" id="keycard">
        <!-- card flair top -->

        <div class="w-full flex justify-center">
            <svg width="76" height="8" viewBox="0 0 76 8" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect x="0.616211" y="0.6875" width="75" height="7" fill="url(#paint0_linear_1122_4658)" />
                <defs>
                    <linearGradient id="paint0_linear_1122_4658" x1="49.0186" y1="1.99857" x2="48.7752" y2="10.6517"
                        gradientUnits="userSpaceOnUse">
                        <stop offset="0.0300935" stop-color="#B0905A" />
                        <stop offset="1" stop-color="#8E5B00" />
                    </linearGradient>
                </defs>
            </svg>
        </div>

        <!-- Close button -->
        <div class="relative top-2 right-2 flex justify-end ">
            <a href="#stay">
                <button @click="closedetails">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                        class="bg-gray-200 rounded- m-2">
                        <path d="M18 6 6 18"></path>
                        <path d="m6 6 12 12"></path>
                    </svg>
                </button>
            </a>
        </div>

        <div class=" flex flex-col lg:flex-row justify-between items-center p-6 lg:gap-6">
            <!-- Key Image -->
            <img :src="keycard.image" alt="Access Key" class="h-130 object-cover rounded-xl w-170 lg:m-10" />
            <div class="flex flex-col items-start justify-between w-full gap-6">
                <div class="flex justify-between items-center w-full">
                    <h1 class="text-3xl py-6" :class="{ 'rudra': keycard.premium }">
                        {{ keycard.name }}
                    </h1>
                    <div class="flex gap-2 lg:pr-15 lg:w-auto w-full justify-end">
                        <svg v-for="_ in keycard.capacity" width="33" height="32" viewBox="0 0 33 32" fill="none"
                            xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M26.7616 27.9721V25.33C26.7616 23.9286 26.2049 22.5845 25.2139 21.5935C24.2229 20.6025 22.8788 20.0458 21.4774 20.0458H10.9089C9.50741 20.0458 8.16334 20.6025 7.17235 21.5935C6.18137 22.5845 5.62463 23.9286 5.62463 25.33V27.9721"
                                stroke="black" stroke-width="2.64212" stroke-linecap="round" stroke-linejoin="round" />
                            <path
                                d="M16.1932 14.76C19.1116 14.76 21.4774 12.3942 21.4774 9.47578C21.4774 6.55737 19.1116 4.19153 16.1932 4.19153C13.2748 4.19153 10.9089 6.55737 10.9089 9.47578C10.9089 12.3942 13.2748 14.76 16.1932 14.76Z"
                                stroke="black" stroke-width="2.64212" stroke-linecap="round" stroke-linejoin="round" />
                        </svg>
                    </div>
                </div>
                <div class="flex flex-wrap gap-2 w-full">
                    <span v-for="tag in keycard.tags"
                        class="border border-yellow-700 text-black text-[12px] font-semibold px-3 py-2 rounded-full">
                        {{ tag }}
                    </span>
                </div>
                <div class="h-[0.5px] bg-black opacity-15 lg:w-11/12 w-full" />
                <div>
                    <p class="text-gray-700 lg:text-xl/10 prata text-ellipsis w-11/12">
                        {{ keycard.desc }}
                    </p>
                    <p class="text-xl font-semibold text-gray-400 pt-10">Diamentions: {{ keycard.diamensions }}</p>
                </div>
                <div class="w-full flex items-center justify-around">
                    <p class="text-2xl font-semibold">
                        {{ keycard.cost }}
                    </p>
                    <a :href="keycard.link">
                        <button
                            class="lg:w-80 py-3 px-4 rudrabg grow-0 shrink-0 text-white font-regular text-xl rounded-lg transition-colors duration-200">
                            Book Now
                        </button>
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
interface KeyCardData {
    name: string;
    image: string;
    capacity: number;
    premium: boolean;
    desc: string;
    diamensions: string;
    tags: Array<string>;
    cost: string;
    link: string;
}

export default {
    props: {
        keycard: {
            type: Object as () => KeyCardData,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    methods: {
        closedetails() {
            const keycard = document.getElementById(this.index.toString());
            const card = document.getElementById('card' + this.index.toString());
            card?.classList.toggle('hidden');
            keycard?.classList.toggle('hidden');

        }
    }
}
</script>

<style scoped>
.rudra {
    color: #B0905A;
}

.rudrabg {
    background-color: #B0905A;
}

.prata {
    font-family: 'Prata', serif;
}
</style>
<template>
    <div class="overflow-hidden max-w-md mx-auto border-[0.5px] border-gray-400" :id="'card' + index">
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
        <!-- Room Image -->
        <div class="relative w-full flex justify-center
         p-10 pb-0">
            <img :src="room.image" alt="Double Bed Room" class=" h-60 object-cover rounded-xl w-90 " />
        </div>


        <div class="flex flex-col justify-center items-center w-full">
            <p :class="{ 'text-2xl lg:text-3xl py-6': true, 'rudra': room.premium }">{{ room.name }}</p>
            <div class="h-[0.5px] bg-black opacity-15 w-11/12" />

        </div>

        <!-- Room Details -->
        <div class="p-6 space-y-4 flex flex-col items-center pb-10">

            <p class="text-gray-700 lg:text-center text-sm lg:text-xl prata lg:truncate text-ellipsis w-11/12">
                {{ room.desc }}
            </p>

            <button class="font-semibold rudra text-xl lg:block hidden " @click="detail">Read More</button>

            <div class="flex flex-wrap gap-2">
                <span v-for="tag in room.tags"
                    class="border border-yellow-700 text-black text-[12px] font-semibold px-3 py-2 rounded-full">
                    {{ tag }}
                </span>

            </div>

            <div class="flex">
                <svg v-for="_ in room.capacity" width="33" height="32" viewBox="0 0 33 32" fill="none"
                    xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M26.7616 27.9721V25.33C26.7616 23.9286 26.2049 22.5845 25.2139 21.5935C24.2229 20.6025 22.8788 20.0458 21.4774 20.0458H10.9089C9.50741 20.0458 8.16334 20.6025 7.17235 21.5935C6.18137 22.5845 5.62463 23.9286 5.62463 25.33V27.9721"
                        stroke="black" stroke-width="2.64212" stroke-linecap="round" stroke-linejoin="round" />
                    <path
                        d="M16.1932 14.76C19.1116 14.76 21.4774 12.3942 21.4774 9.47578C21.4774 6.55737 19.1116 4.19153 16.1932 4.19153C13.2748 4.19153 10.9089 6.55737 10.9089 9.47578C10.9089 12.3942 13.2748 14.76 16.1932 14.76Z"
                        stroke="black" stroke-width="2.64212" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
            </div>

            <p class="text-xl font-semibold ">{{ room.cost }}</p>
            <a href="https://bookings.rudragroups.org">

                <button
                    class="w-2/4 py-3 px-4 rudrabg text-white font-regular text-xl rounded-lg transition-colors duration-200">
                    Book Now
                </button>
            </a>
        </div>
    </div>
</template>

<script lang="ts">
interface RoomData {
    name: string;
    image: string;
    capacity: number;
    premium: boolean;
    desc: string;
    tags: Array<string>;
    cost: string;
}

export default {
    props: {
        room: {
            type: Object as () => RoomData,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    methods: {
        detail() {
            const card = document.getElementById('card' + this.index.toString());
            const keycard = document.getElementById(this.index.toString());

            card?.classList.toggle('hidden');
            keycard?.classList.toggle('hidden');
        }

    }
}

</script>
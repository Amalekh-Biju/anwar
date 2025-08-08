<template>
    <div class="overflow-hidden max-w-md mx-auto border-[0.5px] border-gray-400 bg-white" :id="'card' + index">
        <!-- card flair top -->
        <div class="w-full flex justify-center">
            <svg width="76" height="8" viewBox="0 0 76 8" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect x="0.616211" y="0.6875" width="75" height="7" fill="url(#paint0_linear_1122_4658)" />
                <defs>
                    <linearGradient id="paint0_linear_1122_4658" x1="49.0186" y1="1.99857" x2="48.7752" y2="10.6517"
                        gradientUnits="userSpaceOnUse">
                        <stop offset="0.0300935" stop-color="#1E40AF" />
                        <stop offset="1" stop-color="#059669" />
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
            <p :class="{ 'text-2xl lg:text-3xl py-6': true, 'anwar': room.premium }">{{ room.name }}</p>
            <div class="h-[0.5px] bg-black opacity-15 w-11/12" />

        </div>

        <!-- Room Details -->
        <div class="p-6 space-y-4 flex flex-col items-center pb-10">

            <p class="text-gray-700 lg:text-center text-sm lg:text-xl prata truncate text-ellipsis w-11/12">
                {{ room.desc }}
            </p>

            <div class="flex flex-wrap gap-2">
                <span v-for="(tag, index) in room.tags.slice(0, 3)"
                    class="border border-blue-600 text-black text-[12px] font-semibold px-3 py-2 rounded-full">
                    {{ tag }}
                </span>

            </div>

            <p class="text-xl font-semibold ">{{ room.cost }}</p>
            <a :href="'#'+index" class="w-full flex items-center justify-center">   
                <button @click="detail"
                class="w-2/4 py-3 px-4 anwarbg text-white font-regular text-xl rounded-lg transition-colors duration-200">
                Read More
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
    link: string;
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
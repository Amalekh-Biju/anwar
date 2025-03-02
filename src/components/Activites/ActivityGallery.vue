<template>
    <div class="relative w-full overflow-x-auto overflow-y-hidden scrollbar-hide">
        <div class="flex space-x-4 md:space-x-8 px-4 md:px-6 py-4">
            <div v-for="(key, index) in keywords" :key="index" class="flex-none">
                <img :src="key[0]"
                    class="w-[280px] md:w-[48rem] h-60 md:h-96 object-cover rounded-lg md:rounded-xl shadow-md"
                    :alt="`Gallery image ${index + 1}`" />
                <p class="text-center text-base md:text-xl mt-3 font-medium">
                    {{ key[1]}}
                </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        images: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            keywords: [
                ["/activites/kayaking.jpg","Kayaking"],
                ["/activites/backwater.jpg","Backwater tours"],
                ["/activites/naturetrail.jpg","⁠Nature Trail walk"],
                ["/activites/cycling.jpg","Cycling"],
                ["/activites/spa.jpg","Ayurvedic Spa"],
                ["/activites/bike.webp","Bike rentals"]
            ],
        };
    }
}
</script>
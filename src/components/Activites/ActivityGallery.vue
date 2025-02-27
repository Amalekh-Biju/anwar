<template>
    <div class="relative w-full overflow-x-auto overflow-y-hidden scrollbar-hide">
        <div class="flex space-x-4 md:space-x-8 px-4 md:px-6 py-4">
            <div 
                v-for="(image, index) in images" 
                :key="index" 
                class="flex-none"
            >
                <img 
                    :src="image" 
                    class="w-[280px] md:w-[48rem] h-60 md:h-96 object-cover rounded-lg md:rounded-xl shadow-md" 
                    :alt="`Gallery image ${index + 1}`"
                />
                <p class="text-center text-base md:text-xl mt-3 font-medium">
                    {{ getUniqueKeyword(index) }}
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
                'Luxury Stay',
                'Antique Astethics',
                'Modern Amenities',
                'Rustic Charm',
                'Eco-Friendly',
                'Family Friendly'
            ],
            usedKeywords: [],
        };
    },
    methods: {
        getUniqueKeyword(index) {
            if (index >= this.keywords.length) {
                return this.keywords[index % this.keywords.length];
            }
            
            const availableKeywords = this.keywords.filter(k => !this.usedKeywords.includes(k));
            if (availableKeywords.length === 0) {
                this.usedKeywords = []; // Reset if all keywords are used
                return this.getUniqueKeyword(index);
            }
            
            const keyword = availableKeywords[0];
            this.usedKeywords.push(keyword);
            return keyword;
        }
    }
}
</script>
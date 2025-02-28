<template>
    <div class="relative w-full overflow-x-auto overflow-y-hidden scrollbar-hide">
        <div class="flex space-x-4 md:space-x-8 px-4 md:px-6 py-4">
            <div v-for="(key, index) in keywords" :key="index" class="flex-none">
                <img :src="key"
                    class="w-[280px] md:w-[48rem] h-60 md:h-96 object-cover rounded-lg md:rounded-xl shadow-md"
                    :alt="`Gallery image ${index + 1}`" />
                
            </div>
        </div>
    </div>
</template>

<script>
import data from '../../data/propertydata.json';
export default {
    data() {
        return {
            keywords: data.image
        };
    }
}
</script>
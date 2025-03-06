<template>
    <div class=" flex flex-col gap-3 border-[1px] border-black p-4 lg:w-80 lg:h-80 w-60 h-60 bg-white">
        <div class="flex items-center gap-5">
            <img :src=review.image class="h-10 w-10 rounded-full hidden lg:block" alt="">
            <div>
                <h1 class="text-md lg:text-xl font-semibold">{{ review.name }}</h1>
                <h1>Local Guide</h1>
            </div>
        </div>

        <div class="flex lg:py-2 gap-2">
            <div v-for="i in 5" class="flex">
                <svg  v-if="i<=review.rating" class="w-5 lg:w-10" width="39" height="38" viewBox="0 0 39 38" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M17.1556 2.8071C17.9551 0.346531 21.4361 0.346532 22.2356 2.8071L24.914 11.0503C25.2715 12.1507 26.297 12.8958 27.454 12.8958L36.1215 12.8958C38.7087 12.8958 39.7844 16.2064 37.6913 17.7272L30.6791 22.8218C29.7431 23.5018 29.3514 24.7073 29.709 25.8077L32.3873 34.051C33.1868 36.5115 30.3706 38.5576 28.2775 37.0369L21.2654 31.9423C20.3293 31.2622 19.0618 31.2622 18.1258 31.9423L11.1136 37.0369C9.02056 38.5577 6.20434 36.5115 7.00382 34.051L9.68221 25.8077C10.0398 24.7073 9.64807 23.5018 8.71201 22.8218L1.6999 17.7272C-0.393191 16.2064 0.682513 12.8958 3.26971 12.8958L11.9372 12.8958C13.0942 12.8958 14.1196 12.1507 14.4772 11.0503L17.1556 2.8071Z"
                        fill="url(#paint0_linear_1122_5182)" />
                    <defs>
                        <linearGradient id="paint0_linear_1122_5182" x1="27.2295" y1="4.69681" x2="9.51514" y2="63.4763"
                            gradientUnits="userSpaceOnUse">
                            <stop offset="0.0300935" stop-color="#B0905A" />
                            <stop offset="1" stop-color="#8E5B00" />
                        </linearGradient>
                    </defs>
                </svg>

                <svg v-if="i>review.rating" class="w-5 lg:w-10" width="39" height="38" viewBox="0 0 39 38" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M16.8292 2.8071C17.6286 0.346531 21.1097 0.346532 21.9092 2.8071L24.5876 11.0503C24.9451 12.1507 25.9706 12.8958 27.1276 12.8958L35.795 12.8958C38.3822 12.8958 39.4579 16.2064 37.3648 17.7272L30.3527 22.8218C29.4167 23.5018 29.025 24.7073 29.3825 25.8077L32.0609 34.051C32.8604 36.5115 30.0442 38.5576 27.9511 37.0369L20.939 31.9423C20.0029 31.2622 18.7354 31.2622 17.7994 31.9423L10.7872 37.0369C8.69415 38.5577 5.87792 36.5115 6.67741 34.051L9.3558 25.8077C9.71334 24.7073 9.32165 23.5018 8.3856 22.8218L1.37348 17.7272C-0.719607 16.2064 0.356097 12.8958 2.94329 12.8958L11.6107 12.8958C12.7678 12.8958 13.7932 12.1507 14.1508 11.0503L16.8292 2.8071Z"
                        fill="#C0C0C0" />
                </svg>
            </div>

        </div>
        <h1 class="text-2xl font-bold hidden lg:block">Amazing Experience</h1>
        <p class="prata lg:text-xl text-sm">"{{ review.comment }}"</p>

    </div>
</template>

<script lang="ts">

interface Review {
    id: string;
    image: string;
    name: string;
    rating: number;
    comment: string;
}

//  Sample Review
// {
//     "id": "1",
//     "image": "/thejus/Thejus0.jpeg",
//     "name": "Advaith Narayanan",
//     "rating": 3,
//     "comment": "This Place is super spaciouos and the service is great! definitely coming back again"
// }
export default {
    props: {
        review: {
            type: Object as () => Review,
            required: true
        }
    }
}
</script>

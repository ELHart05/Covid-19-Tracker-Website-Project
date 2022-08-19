<template>
    <div
        class="flex flex-col gap-y-3 items-center rounded-sm justify-center p-4 my-2 shadow-md w-[85%] md:w-[40%] md:mx-2 md:my-0">
        <h2 class="font-bold text-xl text-blue-900">{{ Type }}</h2>
        <div class="flex">
            <strong>New:</strong>
            &nbsp;
            <p>{{ numberWithCommas(newValue) }}</p>
        </div>
        <div class="flex">
            <strong>Total:</strong>
            &nbsp;
            <p>{{ numberWithCommas(totalValue) }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'BoxView',
        props: ['Type', 'Color', 'newValue', 'totalValue'],
        methods: {
            numberWithCommas(x) {
                return x.toString().replace(/\B(?<!\.\d*)(?=(\d{3})+(?!\d))/g, ",");
            }
        }
    }
</script>
<template>
    <div class="mt-6 mb-6 flex md:flex-row flex-col justify-center items-center text-center">
        <BoxView :newValue="allInfo.newConfirmed" :totalValue="allInfo.totalConfirmed" :Type="'Cases'"
            class="bg-blue-100" />
        <BoxView :newValue="allInfo.newDeaths" :totalValue="allInfo.totalDeaths" :Type="'Deaths'" class="bg-blue-200" />
    </div>
</template>

<script>
    import BoxView from './DataField/BoxView.vue';
    export default {
        components: {
            BoxView
        },
        props: ['allInfo']
    }
</script>
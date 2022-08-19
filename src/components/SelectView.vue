<template>
    <select class="border form-select font-bold md:w-[81.5%] w-[85%] border-zinc-500 p-1" v-model="select"
        @change="exportValue">
        <option value="0">Select Country</option>
        <option v-for="country in Countries" :key="country.ID" :value="Countries.indexOf(country)+1">
            {{ country.Country }}</option>
    </select>
</template>

<script>
    export default {
        name: 'SelectView',
        props: ['Countries', 'Title'],
        data() {
            return {
                select: '0'
            }
        },
        methods: {
            exportValue() {
                this.$emit('haltSelect', this.select);
            }
        },
        emits: ['haltSelect']
    }
</script>
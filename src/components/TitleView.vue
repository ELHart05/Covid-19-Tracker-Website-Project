<template>
    <h2 class="font-bold text-xl">{{ Title }}</h2>
    <p class="mt-2">{{ dateFormat }}</p>
</template>

<script>
    import moment from 'moment'

    export default {
        name: 'TitleView',
        props: ['Title', 'Time'],
        computed: {
            dateFormat() {
                return moment(this.Time).format('MMMM Do YYYY, h:mm:ss a');
            }
        }
    }
</script>
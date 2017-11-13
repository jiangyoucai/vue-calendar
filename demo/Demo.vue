<template lang="html">
    <div class="">
        <input class="input" type="text" v-model="date" readonly="readonly" @click="show = 1">
        <v-calendar
           :show="show"
           :date="date"
           v-model="date"
           @close="show = 0">
        </v-calendar>
        {{date}}
    </div>
</template>

<script>
import Calendar from './Calendar'
export default {
    data() {
        return {
            show: 1,
            date: '2017-04-04'
        }
    },
    computed: {},
    created() {},
    methods: {},
    components: {
        'v-calendar': Calendar
    }
}
</script>

<style lang="css" scoped>
</style>

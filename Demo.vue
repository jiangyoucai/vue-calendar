<template lang="html">
    <div class="">
        <v-calendar
            :show="show"
            :date="checked"
            v-model="checked">
         </v-calendar>
        {{checked}}
    </div>
</template>

<script>
import Calendar from './Calendar'
export default {
    data() {
        return {
            show: 1,
            checked: '2016-10-22'
        }
    },
    computed: {},
    watch: {
        checked() {
            this.show = 0
        }
    },
    created() {},
    methods: {},
    components: {
        'v-calendar': Calendar
    }
}
</script>

<style lang="css" scoped>
</style>

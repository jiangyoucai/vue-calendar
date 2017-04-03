# vue-calendar
a calendar for vue2.0

#### how to use

template

    <v-calendar
    :show="show"
    :date="date"
    :checked="date"
    @close="show = 0"></v-charts>

import

    import Calendar from './Calendar'
    export default {
        data() {
            return {
                show: 1,
                date: '2016-10-22'
            }
        },
        computed: {},
        created() {},
        methods: {},
        components: {
            'v-calendar': Calendar
        }
    }

remark

    check the demo or create a issues

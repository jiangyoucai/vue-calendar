# vue-calendar
a calendar for vue2.0

#### how to use

template

    <v-calendar
    :show="show"
    :date="checked"
    :checked="checked"></v-charts>

import

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

remark

    check the demo or create a issues

# vue-calendar
a calendar for vue2.0

#### how to use

template

    <input class="input" type="text" v-model="date" readonly="readonly" @click="show = 1">
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

screenshot

![pc](http://static.ipanpan.com/ipanpan/file_1491235270224918844.jpg)
![mobile](http://static.ipanpan.com/ipanpan/file_1491235281237544823.jpg)

remark

    check the demo or create a issues

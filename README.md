# vue-calendar
a calendar for vue2.0

#### install

npm

    npm install tt-vue-calendar

yarn 

    yarn add tt-vue-calendar

#### how to use

template

    <input class="input" type="text" v-model="date" readonly="readonly" @click="show = 1">
    <v-calendar
    :show="show"
    :date="date"
    :checked="date"
    @close="show = 0"></v-calendar>

script

    import Calendar from 'tt-vue-calendar'
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

screenshot

![pc](http://static.ipanpan.com/ipanpan/file_1491235270224918844.jpg)
![mobile](http://static.ipanpan.com/ipanpan/file_1491235281237544823.jpg)

remark

    check the demo or create a issues

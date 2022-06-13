# vue calendar
a calendar component for vue3.0

## how to use

template 

```html
<template>
    <div class="container y35 ym20 fs12 cl6 t-pointer x-row x-between">
        <!-- date -->
        <div class="x10">
            <Date
                class="x100 y35 fs12 bgf br4 bcz b-border b-box t-center"
                :calendar="date.calendar"
                :style="date.style"
                @submit="getDate"
            ></Date>
        </div>

        <!-- time -->
        <div class="x15">
            <Time
                class="x100 y35 fs12 bgf br4 bcz b-border b-box t-center"
                :calendar="time.calendar"
                :style="time.style"
                @submit="getTime"
            ></Time>
        </div>
    </div>
</template>
```


```html
<script>
import { reactive, toRefs } from "@vue/runtime-core";
import Date from "./Date.vue";
import Time from "./Time.vue";
export default {
    setup(props, context) {
        const data = reactive({
            date: {
                style: "width:266%;",
                calendar: {
                    mulit: false,
                    mark: "今",
                    disable: undefined,
                    show: undefined,
                },
            },
            time: {
                style: "width:176%;",
                calendar: {
                    mulit: true,
                    mark: "今",
                    disable: undefined,
                    show: undefined,
                },
            },
        });

        const getDate = (option) => {
            submit(3, option);
        };

        const getTime = (option) => {
            submit(4, option);
        };

        return {
            ...toRefs(data),
            getDate,
            getTime,
        };
    },
    components: {
        Date,
        Time,
    },
};
</script>
```


```html
<style scoped>
@import "../assets/css/base.css";
@import "../assets/css/flex.css";
</style>
```

#### single date

    date: {
        style: "width:266%;",
        calendar: {
            mulit: false,
            mark: "今",
            disable: undefined,
            show: undefined,
            date: "2021-03-06",
        },
    }

#### mulit date

    time: {
    style: "width:176%;",
    calendar: {
        mulit: true,
        mark: "今",
        disable: undefined,
        show: undefined,
        start: "2021-03-06",
        end: "2021-03-07",
    },


## more config

    option: {
        mulit: false,
        mark: '今',
        disable: 'left',
        // show: 'fee',
        empty: false,
        total: {
            '2020-9-27': 99,
            '2020-9-28': 9,
            '2020-9-29': 1024,
            '2020-9-30': 0,
            '2020-10-27': 99,
            '2020-10-28': 9,
            '2020-10-29': 1024,
            '2020-10-7': 0,
            '2020-10-8': 9,
            '2020-10-9': 10204,
        },
        fee: {
            '2020-9-27': 99,
            '2020-9-28': 9,
            '2020-9-29': 1024,
            '2020-9-30': 0,
            '2020-10-27': 99,
            '2020-10-28': 9,
            '2020-10-29': 10204,
            '2020-10-7': 0,
            '2020-10-8': 9,
            '2020-10-9': 1024,
        },
        customize: {
            '2020-9-27': '休',
            '2020-9-28': '班',
            '2020-9-29': '休',
            '2020-10-7': '休',
            '2020-10-8': '初八',
            '2020-10-9': '初九',
        }
    }

## methods

1.setDate

    setDate: function (e) {
        console.log(e)
    }
    
2.setDay

    setDay: function (e) {
        console.log(e)
    }
   

## screenshot

![普通日历](http://cdn.tiantour.com/screenshot/normal.png)

![库存日历](http://cdn.tiantour.com/screenshot/total.png)

![价格日历](http://cdn.tiantour.com/screenshot/fee.png)

![自定义日历](http://cdn.tiantour.com/screenshot/customize.png)

## remark

    check the demo or create a issues

<template>
<div class="container" transition="fade" v-if="show" @input="checked" @click="checked">
    <div class="calendar" @click="stopPop($event)">
        <div class="month">
            <div class="arrowWrap arrowWrap-left" @click="monthPre">
                <i class="arrow arrow-left"></i>
            </div>
            <p>{{ year }}年{{ month + 1}}月</p>
            <div class="arrowWrap arrowWrap-right" @click="monthNext">
                <i class="arrow arrow-right"></i>
            </div>
        </div>
        <div class="week">
            <p :class="{'weekend': index ==0 || index == 6}" v-for="(item,index) in week">
                {{item}}
            </p>
        </div>
        <div class="day">
            <p v-for="(item,index) in calendar">
                <span v-if="item!==0" :class="{'disabled':item<day,'current':item===day}" @click="checkDate(index)">
                        {{item}}
                    </span>
                <span v-else>&nbsp;</span>
            </p>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            year: 0,
            month: 0,
            day: 0,
            calendar: []
        }
    },
    created() {
        const now = new Date(this.date)
        this.year = now.getFullYear()
        this.month = now.getMonth()
        this.day = now.getDate()
        this.setDate()
    },
    props: {
        show: {
            required: true,
            twoWay: true
        },
        date: {
            required: true,
            twoWay: true,
            default: () => new Date()
        },
        week: {
            type: Array,
            default: () => ['日', '一', '二', '三', '四', '五', '六']
        }
    },
    methods: {
        weekIndex(year, month, day) {
            return new Date(year, month, day).getDay()
        },
        monthCount(year, month) {
            return new Date(year, month + 1, 0).getDate()
        },
        monthPre() {
            if (this.month === 0) {
                this.year -= 1
                this.month = 12
            }
            this.month -= 1
            this.setDate()
            this.day = 1
        },
        monthNext() {
            if (this.month === 11) {
                this.year += 1
                this.month = -1
            }
            this.month += 1
            this.day = 1
            this.setDate()
        },
        setDate() {
            this.calendar = []
            const start = this.weekIndex(this.year, this.month, 1)
            let count = this.monthCount(this.year, this.month)
            if (start !== 0) {
                count += start
            }
            for (let i = 0; i <= count; i++) {
                if (i < start) {
                    this.$set(this.calendar, i - 1, 0)
                } else {
                    this.$set(this.calendar, i - 1, i - start)
                }
            }
        },
        checkDate(index) {
            this.day = this.calendar[index]
            this.checked()
        },
        stopPop($event) {
            $event.stopPropagation()
        },
        checked() {
            const date = this.year + '-' + this.completion(this.month + 1) + '-' + this.completion(this.day)
            this.$emit('input', date)
        },
        completion(data) {
            return data < 10 ? ('0' + data) : data
        }
    }
}
</script>
<style lang="css" scoped>
.container {
    position: fixed;
    width: 100%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 999;
    background-color: rgba(0, 0, 0, .5);
}
.calendar {
    position: absolute;
    bottom: 0;
    background-color: #FFF;
    font-size: 1rem;
    color: #666;
    width: 100%;
}
.month {
    position: relative;
    text-align: center;
    height: 50px;
    line-height: 50px;
}
.month .arrowWrap {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 50px;
}
.month .arrowWrap-right {
    left: auto;
    right: 0;
}
.month .arrow {
    position: absolute;
    left: 50%;
    display: block;
    width: 8px;
    height: 8px;
    margin: 20px 0;
    border-top: 2px solid #DE3378;
    border-right: 2px solid #DE3378;
    transform: rotate(-135deg);
    -webkit-transform: rotate(-135deg);
}
.month .arrow-right {
    right: 50%;
    left: auto;
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
}
.week,.day{
    padding:  0 1vw;
}
.week{
    height: 6vh;
    line-height: 6vh;
    background: #F5F5F5;
}
.week .weekend {
    color: #DE3378;
}
.week p,
.day  p {
    float: left;
    width: 14vw;
    height: 4vh;
    line-height: 4vh;
    margin: 1vh 0;
    text-align: center;
}
.day .disabled{
    color: #999;
}
.day .current{
    background: #DE3378;
    color: #FFF;
    width: 4vh;
    border-radius: 2vh;
    display: block;
    margin: auto;
}
</style>

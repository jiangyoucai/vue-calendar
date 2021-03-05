<template >
    <div class="bgf">
        <!-- action -->
        <p class="container y40 t-center">
            <span class="x10"></span>
            <!-- year - -->
            <span class="x10" v-if="option.show !== undefined"></span>
            <span class="x10 fs16 cl6 t-pointer" @click="setYear(-1)" v-else>
                {{ left.year }}
            </span>
            <!-- month - -->
            <span class="x10 fs16 cl6 t-pointer" @click="setMonth(-1)">
                {{ left.month }}
            </span>
            <!-- current -->
            <span class="x50">{{ year }} 年 {{ month }} 月</span>
            <!-- month + -->
            <span class="x10 fs16 cl6 t-pointer" @click="setMonth(1)">
                {{ right.month }}
            </span>
            <!-- year + -->
            <span class="x10" v-if="option.show !== undefined"> </span>
            <span class="x10 fs16 cl6 t-pointer" @click="setYear(1)" v-else>
                {{ right.year }}
            </span>
            <span class="x10"></span>
        </p>
        <!-- week -->
        <p class="container bgfa cl6 x-warp t-center">
            <span class="x10 xm2 y40" v-for="(v, k) in week" :key="k">{{
                v
            }}</span>
        </p>
        <!-- date -->
        <div class="container x-warp t-center">
            <!-- pre month -->
            <div class="x10 xm2 ym5" v-for="(v, k) in min" :key="k + max">
                <span class="y25"></span>
            </div>
            <!-- current month -->
            <div class="x10 xm2 ym5" v-for="(v, k) in max" :key="k">
                <!-- disable left -->
                <p
                    class="container x-column"
                    v-if="option.disable === 'left' && setLess(v)"
                >
                    <span class="y25 cl9 x-center">{{ setText(v) }}</span>
                    <!-- show -->
                    <span v-if="option.show !== undefined">
                        <em class="y25"></em>
                    </span>
                </p>
                <!-- disable right -->
                <p
                    class="container x-column"
                    v-else-if="option.disable === 'right' && setMore(v)"
                >
                    <span class="y25 cl9 x-center">{{ setText(v) }}</span>
                    <!-- show -->
                    <span v-if="option.show !== undefined">
                        <em class="y25"></em>
                    </span>
                </p>
                <!-- enable day -->
                <p class="container x-column" v-else>
                    <!-- show not set -->
                    <span
                        class="container x-center t-pointer"
                        v-if="!option.show"
                    >
                        <em
                            class="w25 y25 brx"
                            :class="setStyle(v) ? 'bgx clf' : ''"
                            @click="setDate(v)"
                            >{{ setText(v) }}</em
                        >
                    </span>
                    <!-- fee -->
                    <span
                        class="container x-center t-pointer"
                        v-if="option.show === 'fee'"
                    >
                        <em
                            class="w25 y25 brx"
                            :class="setStyle(v) ? 'bgx clf' : ''"
                            v-if="setFee(v)"
                            @click="setDate(v)"
                            >{{ setText(v) }}</em
                        >
                        <em class="y25 cl9" v-else>{{ setText(v) }}</em>
                    </span>
                    <!-- fee -->
                    <span
                        class="container x-center t-pointer"
                        v-if="option.show === 'fee'"
                    >
                        <em class="y25 fs12 clx" v-if="!setFee(v)"></em>
                        <em class="y25 fs12 clx" v-else-if="setFee(v) <= 0"
                            >售罄</em
                        >
                        <em class="y25 fs12 clx" v-else-if="setFee(v) >= 9999"
                            >￥9999+</em
                        >
                        <em class="y25 fs12 clx" v-else>￥{{ setFee(v) }}</em>
                    </span>
                    <!-- total -->
                    <span
                        class="container x-center t-pointer"
                        v-if="option.show === 'total'"
                    >
                        <em
                            class="w25 y25 brx"
                            :class="setStyle(v) ? 'bgx clf' : ''"
                            v-if="setTotal(v)"
                            @click="setDate(v)"
                            >{{ setText(v) }}</em
                        >
                        <em class="y25 cl9" v-else>{{ setText(v) }}</em>
                    </span>
                    <!-- total -->
                    <span
                        class="container x-center t-pointer"
                        v-if="option.show === 'total'"
                    >
                        <em class="y25 fs12 clx" v-if="!setTotal(v)"></em>
                        <em class="y25 fs12 clx" v-else-if="setTotal(v) <= 0"
                            >售罄</em
                        >
                        <em class="y25 fs12 clx" v-else-if="setTotal(v) >= 99"
                            >充足</em
                        >
                        <em class="y25 fs12 clx" v-else>{{ setTotal(v) }}件</em>
                    </span>
                    <!-- customize -->
                    <span
                        class="container x-center t-pointer"
                        v-if="option.show === 'customize'"
                    >
                        <em
                            class="w25 y25 brx"
                            :class="setStyle(v) ? 'bgx clf' : ''"
                            v-if="setCustomize(v)"
                            @click="setDate(v)"
                            >{{ setText(v) }}</em
                        ><em class="y25 cl9" v-else>{{ setText(v) }}</em>
                    </span>
                    <!-- customize -->
                    <span
                        class="container x-center t-pointer"
                        v-if="option.show === 'customize'"
                    >
                        <em class="y25 fs12 clx" v-if="!setCustomize(v)"></em>
                        <em class="y25 fs12 clx" v-else>{{
                            setCustomize(v)
                        }}</em>
                    </span>
                </p>
            </div>
        </div>
    </div>
</template>
<script>
import { reactive, ref } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
export default {
    props: {
        option: {
            type: Object,
            value: {
                // bool, 默认undefined，可选true, false
                mulit: undefined,
                // str, 默认undefined, 可选汉字/英文
                mark: undefined,
                // str, 默认undefined，可选left, right
                disable: undefined,
                // str, 默认undefined, 可选total, fee, customize
                show: undefined,
                // object, 默认undefined
                total: undefined,
                // object, 默认undefined
                fee: undefined,
                // object, 默认undefined
                customize: undefined,
                // str, 默认undefined
                date: undefined,
                // str, 默认undefined
                start: undefined,
                // str, 默认undefined
                end: undefined,
            },
        },
    },
    setup(props, context) {
        // map, 默认year, month
        const left = reactive({
            year: "<<",
            month: "<",
        });
        // map, 默认year, month
        const right = reactive({
            year: ">>",
            month: ">",
        });
        // int, 默认当前时间
        const now = computed(() => {
            if (props.option.mulit) {
                props.option.start ? new Date(props.option.start) : new Date();
            }
            return props.option.date ? new Date(props.option.date) : new Date();
        });
        // int, 默认当前年
        const year = ref(now.value.getFullYear());
        // int, 默认当前月
        const month = ref(now.value.getMonth() + 1);
        // list, 默认周日开始，周六结束
        const week = ref(["日", "一", "二", "三", "四", "五", "六"]);
        // int, 默认月初是周几
        const min = ref(new Date(year.value, month.value - 1, 1).getDay());
        // int, 默认月末是几号
        const max = ref(new Date(year.value, month.value, 0).getDate());
        // map, 默认当前年, 月, 日
        const current = reactive({
            year: new Date().getFullYear(),
            month: new Date().getMonth() + 1,
            date: new Date().getDate(),
        });
        // map, 默认选中日期，开始日期，结束日期
        const select = reactive({
            date: {
                year: props.option.date
                    ? new Date(props.option.date).getFullYear()
                    : 0,
                month: props.option.date
                    ? new Date(props.option.date).getMonth() + 1
                    : 0,
                date: props.option.date
                    ? new Date(props.option.date).getDate()
                    : 0,
            },
            start: {
                year: props.option.start
                    ? new Date(props.option.start).getFullYear()
                    : 0,
                month: props.option.start
                    ? new Date(props.option.start).getMonth() + 1
                    : 0,
                date: props.option.start
                    ? new Date(props.option.start).getDate()
                    : 0,
            },
            end: {
                year: props.option.end
                    ? new Date(props.option.end).getFullYear()
                    : 0,
                month: props.option.end
                    ? new Date(props.option.end).getMonth() + 1
                    : 0,
                date: props.option.end
                    ? new Date(props.option.end).getDate()
                    : 0,
            },
        });

        const setYear = (index) => {
            year.value += parseInt(index);
            setDay();
        };

        const setMonth = (index) => {
            month.value += parseInt(index);
            // less than
            if (month.value < 1) {
                year.value--;
                month.value = 12;
            }
            // more than
            if (month.value > 12) {
                year.value++;
                month.value = 1;
            }
            setDay();
        };

        const setDay = () => {
            // 计算，月初对应的星期
            min.value = new Date(year.value, month.value - 1).getDay();
            // 计算，月未对应的数字
            max.value = new Date(year.value, month.value, 0).getDate();
            context.emit("setDay", {
                year: year.value,
                month: month.value,
                min: 1,
                max: max.value,
            });
        };

        const setDate = (index) => {
            if (props.option.mulit) {
                // 多选
                // 1. 首次选中
                // 设置start
                // 2. 第N次选中
                // 当选中日期<start，则start向左移动
                // 当选中日期>start，则end向右移动

                // 开始日期
                const start = new Date(
                    select.start.year,
                    select.start.month,
                    select.start.date
                ).getTime();

                if (start < 0) {
                    // 首次选中
                    select.start = {
                        year: year.value,
                        month: month.value,
                        date: index,
                        format:
                            year.value +
                            "-" +
                            setZero(month.value) +
                            "-" +
                            setZero(index),
                    };
                } else {
                    // 第N次选中
                    // 选中日期
                    const now = new Date(
                        year.value,
                        month.value,
                        index
                    ).getTime();
                    // 判断大小
                    if (now > start) {
                        // end，向右移动
                        select.end = {
                            year: year.value,
                            month: month.value,
                            date: index,
                            format:
                                year.value +
                                "-" +
                                setZero(month.value) +
                                "-" +
                                setZero(index),
                        };
                    } else {
                        // start，向左移动
                        select.start = {
                            year: year.value,
                            month: month.value,
                            date: index,
                            format:
                                year.value +
                                "-" +
                                setZero(month.value) +
                                "-" +
                                setZero(index),
                        };
                    }
                }
            } else {
                // 单选
                select.date = {
                    year: year.value,
                    month: month.value,
                    date: index,
                    format:
                        year.value +
                        "-" +
                        setZero(month.value) +
                        "-" +
                        setZero(index),
                };
            }
            context.emit("setDate", select);
        };

        const setZero = (index) => {
            return index.toString().padStart("2", "0");
        };

        const setLess = (index) => {
            const n = new Date(year.value, month.value, index).getTime();
            const c = new Date(
                current.year,
                current.month,
                current.date
            ).getTime();
            if (n < c) {
                return true;
            }
            return false;
        };

        const setMore = (index) => {
            const n = new Date(year.value, month.value, index).getTime();
            const c = new Date(
                current.year,
                current.month,
                current.date
            ).getTime();
            if (n > c) {
                return true;
            }
            return false;
        };

        const setStyle = (index) => {
            const n = new Date(year.value, month.value, index).getTime();
            const d = new Date(
                select.date.year,
                select.date.month,
                select.date.date
            ).getTime();
            const s = new Date(
                select.start.year,
                select.start.month,
                select.start.date
            ).getTime();
            const e = new Date(
                select.end.year,
                select.end.month,
                select.end.date
            ).getTime();
            if (n === d || n === s || n === e) {
                return true;
            }
            return false;
        };

        const setText = (index) => {
            const n = new Date(year.value, month.value, index).getTime();
            const c = new Date(
                current.year,
                current.month,
                current.date
            ).getTime();
            return n !== c ? index : props.option.mark;
        };

        const setFee = (index) => {
            const n =
                year.value + "-" + setZero(month.value) + "-" + setZero(index);
            return props.option.fee[n];
        };

        const setTotal = (index) => {
            const n =
                year.value + "-" + setZero(month.value) + "-" + setZero(index);
            return props.option.total[n];
        };

        const setCustomize = (index) => {
            const n =
                year.value + "-" + setZero(month.value) + "-" + setZero(index);
            return props.option.customize[n];
        };

        return {
            left,
            right,
            year,
            month,
            week,
            min,
            max,
            current,
            select,
            setYear,
            setMonth,
            setDay,
            setDate,
            setZero,
            setLess,
            setMore,
            setText,
            setStyle,
            setFee,
            setTotal,
            setCustomize,
        };
    },
};
</script>

<style>
</style>
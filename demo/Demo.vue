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

<style scoped>
@import "../assets/css/base.css";
@import "../assets/css/flex.css";
</style>
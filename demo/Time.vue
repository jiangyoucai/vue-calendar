<template>
	<p class="t-pointer p-relative option">
		<em
			>{{
				start ? start : calendar.start ? calendar.start : "开始日期"
			}}
			至 {{ end ? end : calendar.end ? calendar.end : "结束日期" }}
		</em>
		<span
			class="x100 br4 r0 bcz b-border b-box o-hidden p-absolute hidden"
			:style="style ? style : ''"
		>
			<Calendar :option="calendar" @setDate="submit"></Calendar>
		</span>
	</p>
</template>

<script>
import { reactive, toRefs } from "@vue/reactivity";
import Calendar from "../calendar/Calendar";
export default {
	props: {
		calendar: Object,
		style: String,
	},
	setup(props, context) {
		const date = reactive({
			start: "",
			end: "",
		});

		const submit = (option) => {
			date.start = option.start.format;
			date.end = option.end.format;
			context.emit("submit", date);
		};
		return {
			...toRefs(date),
			submit,
		};
	},
	components: {
		Calendar,
	},
};
</script>

<style>
</style>
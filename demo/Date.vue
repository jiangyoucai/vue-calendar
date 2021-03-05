<template>
	<p class="t-pointer p-relative option">
		<em>{{ date ? date : calendar.date ? calendar.date : "出行日期" }}</em>
		<span
			class="x100 br4 r0 bcz b-border b-box o-hidden p-absolute hidden"
			:style="style ? style : ''"
		>
			<Calendar :option="calendar" @setDate="submit"></Calendar>
		</span>
	</p>
</template>

<script>
import { ref } from "@vue/reactivity";
import Calendar from "../calendar/Calendar";
export default {
	props: {
		calendar: Object,
		style: String,
	},
	setup(props, context) {
		const date = ref("");

		const submit = (option) => {
			date.value = option.date.format;
			context.emit("submit", {
				date: date.value,
			});
		};

		return {
			date,
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
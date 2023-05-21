<template lang="pug">
.password-monitor-container {{ password }}

</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
	name: 'PasswordMonitorView',
	props: {
		password: {
			type: String,
			required: true,
		},
	},
});
</script>

<style lang="scss" scoped>
.password-monitor-container {
	background-color: black;
	color: white;
	margin-top: 1rem;
	padding: 1rem;
	border: 1px solid #333;
	height: 2rem;
	width: 350px;
	display: flex;
	justify-content: center;
	align-items: center;
	word-break: break-all;
	border-radius: 0.5rem;
}
</style>

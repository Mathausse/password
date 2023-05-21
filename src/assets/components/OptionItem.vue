<template lang="pug">
label {{ label }}
input(:type='type')
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
	name: 'OptionItemView',
	props: {
		label: null,
		type: {
			type: String,
			required: true,
		},
	},
});
</script>

<style lang="scss"></style>

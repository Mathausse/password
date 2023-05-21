<template lang="pug">
.option-selector-container
    OptionItem(label='Longueur' type='number')
    OptionItem(label='Majuscules' type='checkbox')
    OptionItem(label='Nombres' type='checkbox')
    OptionItem(label='Symboles' type='checkbox')
</template>

<script>
import { defineComponent } from 'vue';
import OptionItem from './OptionItem.vue';

export default defineComponent({
	name: 'OptionSelectorView',
	methods: {},
	components: {
		OptionItem,
	},
});
</script>

<style lang="scss">
.option-selector-container {
	display: grid;
	margin-top: 2rem;
	grid-template-columns: auto auto;
	row-gap: 1rem;
	column-gap: 3rem;
	justify-content: center;
	align-items: center;
}
</style>

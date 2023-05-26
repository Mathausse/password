<template lang="pug">
.option-selector-container
	OptionItem(label='Longueur' type='number' v-model="pwSize")
	OptionItem(label='Majuscules' type='checkbox' v-model="uppercase")
	OptionItem(label='Nombres' type='checkbox' v-model="numbers")
	OptionItem(label='Symboles' type='checkbox' v-model="symbols")
	Button 
</template>

<script>
import { defineComponent } from 'vue';
import OptionItem from './OptionItem.vue';

export default defineComponent({
	name: 'OptionSelectorView',
	methods: {
		generatePassword() {},
	},
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

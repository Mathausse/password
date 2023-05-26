<template lang="pug">
.container
  PasswordMonitor( :password='password')
  OptionSelector

</template>

<script>
import { defineComponent } from 'vue';

import PasswordMonitor from './assets/components/PasswordMonitor.vue';
import OptionSelector from './assets/components/OptionSelector.vue';

export default defineComponent({
	name: 'App',
	components: {
		PasswordMonitor,
		OptionSelector,
	},
	data: function () {
		return {
			MINUSCULE_CODE_CHAR: [],
			MAJUSULE_CODE_CHAR: [],
			NOMBRE_CODE_CHAR: [],
			SYMBOlE_CODE_CHAR: [],
			password: '',
			avecMaj: false,
			avecNom: false,
			avecSym: false,
			taille: 1,
		};
	},
	mounted() {
		this.remplissageListe();
	},
	methods: {
		randomFloat() {
			const int = window.crypto.getRandomValues(new Uint32Array(1))[0];
			return int / 2 ** 32;
		},
		randomInt(range) {
			return Math.floor(this.randomFloat() * range);
		},
		remplissageListe() {
			this.MINUSCULE_CODE_CHAR = this.arrayFromLowToHigh(97, 122);
			this.MAJUSULE_CODE_CHAR = this.arrayFromLowToHigh(65, 90);
			this.NOMBRE_CODE_CHAR = this.arrayFromLowToHigh(48, 57);
			this.SYMBOlE_CODE_CHAR = this.arrayFromLowToHigh(33, 47)
				.concat(this.arrayFromLowToHigh(58, 64))
				.concat(this.arrayFromLowToHigh(91, 96))
				.concat(this.arrayFromLowToHigh(123, 126));
		},
		generationMotDePasse(nbCharactere, majuscule, nombre, symbole) {
			let codeChar = this.MINUSCULE_CODE_CHAR;
			if (majuscule) {
				codeChar = codeChar.concat(this.MAJUSULE_CODE_CHAR);
			}
			if (nombre) {
				codeChar = codeChar.concat(this.NOMBRE_CODE_CHAR);
			}
			if (symbole) {
				codeChar = codeChar.concat(this.SYMBOlE_CODE_CHAR);
			}
			codeChar.sort(function (a, b) {
				return a - b;
			});
			const characteresMotDePasse = [];
			for (let i = 0; i < nbCharactere; i++) {
				const c = codeChar[this.randomInt(codeChar.length)];
				characteresMotDePasse.push(String.fromCharCode(c));
			}
			this.password = characteresMotDePasse.join('');
		},
		arrayFromLowToHigh(min, max) {
			const liste = [];
			for (let i = min; i <= max; i++) {
				liste.push(i);
			}
			return liste;
		},
	},
});
</script>

<style>
body {
	background-color: #283969;
	color: black;
	display: flex;
	justify-content: center;
	align-items: center;
}

h1 {
	margin: 0;
	text-align: center;
	font-weight: bold;
	font-size: 5em;
}

button {
	grid-column: span 2;
	background-color: transparent;
	border: 2px solid white;
	color: black;
	padding: 0.5rem 1rem;
	font-weight: bold;
	cursor: pointer;
	border-radius: 1rem;
}

button:hover {
	background-color: #ffffff33;
}

.container {
	background-color: antiquewhite;
	margin-top: 10vh;
	padding: 3rem;
	border-radius: 1rem;
	border: 2px solid black;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}

.pannel {
	display: grid;
	margin-top: 2rem;
	grid-template-columns: auto auto;
	row-gap: 1rem;
	column-gap: 3rem;
	justify-content: center;
	align-items: center;
}
</style>

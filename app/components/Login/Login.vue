<template src="./Login.html"></template>

<script lang="ts">
import Vue from 'vue'
import { getJSON, getString } from 'tns-core-modules/http'
import { parse } from 'node-html-parser'
const jsdom = require("jsdom");
const { JSDOM } = jsdom;
const $ = require('jquery')

export default Vue.extend({
	data() {
		return {
			unscrambled_words: [],
			loading: false,
			word: 'goe',
			url: 'https://www.wordunscrambler.net'
		}
	},
	methods: {
		/*unscramble() {
			getJSON(`${this.url}?word=${this.word}`).then(res => {
				console.log({
					url: `${this.url}?word=${this.word}`,
					res: res
				});
				this.unscrambled_words = res['data'] || res;
			}, err => console.log(err))*/
		unscramble() {
			getString(`${this.url}?word=${this.word}`).then(res => {
				console.log(res)
				// let html = document.createElement('html');
				// html.innerHTML = res;
				// const parser = new DOMParser();
				const { window } = new JSDOM(res);
				const htmlDoc = parse(res)
				const response = window.$('.word > a')
				// const response = [];
				// const unscrambled = [];
				for (let i = 0; i < response.length; i++) {
					if (response[i].children[0].data.length > 2) {
						this.unscrambled_words.push(response[i].children[0].data)
					}
				}
				console.log('answer', this.unscrambled_words);
			}). catch(err => console.log(err))
		}
		
	}
})
</script>

<style scoped>
	.page {
			align-items: center;
			flex-direction: column;
			justify-content: center;
			background: linear-gradient(to right, #39B994, #337FC7);
	}

	.logo {
			margin-bottom: 40;
			height: 90;
			/* horizontal-alignment: center; */
	}

	.form-input {
			color: black;
			width: 90%;
			placeholder-color: white;
	}

	.border-bottom {
		border-bottom-width: 0;
		border-bottom-color: white;
	}

	.icon-space {
		width: 16;
		height: 16;
		margin-right: 10;
		margin-top: 5;
	}

</style>
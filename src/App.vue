<template>
	<div id="app">
		<header class="container header">
			<h1 class="header__title">Выполненное тестовое задание для BestStocks.ru.</h1>
			<p class="header__subtitle">Форма для вычисления сумм дробей.</p>
			<p class="header__subtitle">Текст <a class="link" href="https://docs.google.com/document/d/1DCtla3uNP_wOeRUuM79TfdTlNcDHmGqvlOjlHhcbp88/edit" target="_blank">тестового задания</a>.</p>
		</header>
		<main class="container main">
			<div class="wrapper">
				<Fraction v-for="(number, index) in numbers" :key="index"
					:number="number"
					:index="index"
					:length="numbers.length"
					@close="close"
				/>
				<div class="result">{{ result }}</div>
			</div>
			<button class="add_button" @click="addFractions">Еще дробь</button>
		</main>
		<footer class="container footer"> <p class="footer__text">Выполнил <a class="link" href="https://github.com/stasokulov" target="_blank">Окулов Станислав</a></p> </footer>
	</div>
</template>

<script>
import Fraction from './components/Fraction.vue'

export default {
  name: 'App',
  components: {
    Fraction
  },
  data() {
	return {
		numbers: [[1, 1], [1, 1]],
		fraction: [1, 1]
	}
  },
  computed: {
	subResult: function() {
		let subResult = this.numbers.map(item => {
				return	item[0]/item[1]*10
			});
		return subResult
	},
	result: function() {
		let result = this.subResult.reduce((sum, current) => sum + current);
		return result/10
	}
  },
  watch: {
	numbers: function() {
		this.numbers.forEach((item, index) => {
			item.forEach((subItem, subIndex) => {			
				this.numbers[index][subIndex] = Math.round(subItem);
				if(subItem.length > 2) {
					this.numbers[index][subIndex] = subItem.slice(0,2);
				}
				if(subItem < 0) {
					this.numbers[index][subIndex] = -subItem;
				}
				if(this.numbers[index][subIndex] === 0) {
					this.numbers[index][subIndex] = 1;
				}
				
			})
		})
	}
  },
  methods: {
	addFractions: function() {
		if(this.numbers.length<5) {
			this.numbers.push([...this.fraction])
		}
	},
	close: function(index) {
		this.numbers.splice(index,1)
	}
  }
}
</script>

<style>
body {
    margin: 0;
    font-family: Arial,Helvetica,sans-serif;
    font-size: 18px;
}
.link {
    color: #bcf;
    text-decoration: none;
}
.container {
    padding-left: 20px;
    padding-right: 20px;
}
.header {
	padding-top: 20px;
	padding-bottom: 10px;
	background-color: #345;
	color: #fff;
}
.header__title {
	margin: 0 0 20px;
	font-size: 22px;
	text-align: center;
}
.header__subtitle {
	margin: 0 0 5px;
	line-height: 1.5;
}
.main {
	margin-bottom: 20px;
}
.wrapper {
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
	padding: 20px 0;
}
.result {
	position: relative;
	display: flex;
	align-items: center;
	font-size: 40px;
}
.result::before {
	content: "=";
	position: absolute;
	top: 50%;
	left: -60px;
	transform: translate(0, -50%);
}
.add_button {
	display: block;
	margin: auto;
	padding: 20px;
	cursor: pointer;
}
footer {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 61px;
    background-color: #345;
    color: #fff;
    text-align: center;
}
</style>

<template>
	<div class="fraction">
		<input class="input top" type="number" min="1" max="99" v-model="number[0]">
		<input class="input bottom" type="number" min="1" max="99" v-model="number[1]">
		<span class="close"
			@click="$emit('close', index)"
			v-if="length > 2"
		>+</span>
	</div>
</template>

<script>
export default {
  name: 'Fraction',
  props: {
    number: Array,
	length: Number,
	index: Number
  }
}
</script>

<style scoped>
.fraction {
	position: relative;
	width: 100px;
	font-size: 40px;
	padding: 20px 0;
}
.fraction:not(:first-child)::before {
	content: "+";
	position: absolute;
	top: 50%;
	left: -50%;
	transform: translate(-50%, -50%);
}
.fraction:not(:last-child) {
	margin-right: 100px;
}
.close {
	position: absolute;
	display: flex;
	top: 0;
	right: -20px;
	justify-content: center;
	align-items: center;
	width: 20px;
	height: 20px;
	transform: rotate(45deg);
	border-radius: 50%;
	font-size: 30px;
	cursor: pointer;
}
.close:hover {
	background-color: beige;
}
.input {
	display: block;
	width: 100%;
	height: 100px;
	box-sizing: border-box;
	text-align: center;
	font-size: 40px;
}
.top {
	margin-bottom: 10px;
}
</style>

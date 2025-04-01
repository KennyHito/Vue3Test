<template>
	<div class="app">
		<div class="div_box">
			<h4>1、学习vue3的ref和reactive</h4>
			<span>我叫:{{ person.firstName }}{{ person.lastName }}</span>
			<span>语文成绩:{{ xLanguage }}</span>
			<span>数学成绩:{{ xMaths }}</span>
			<span>英语成绩:{{ xEnglish }}</span>
			<button @click="changeUserName">看错姓名,应该改为李四</button>
			<button @click="changeEnglishScore">修改英语成绩</button>
		</div>

		<hr />

		<div class="div_box">
			<h4>2、学习vue3的计算属性</h4>
			<div>姓:<input type="text" v-model="person.firstName"></div>
			<div>名:<input type="text" v-model="person.lastName"> </div>
			<div>全名:{{ person.fullName }}</div>
			<div>全名:<input type="text" v-model="person.fullName"></div>
		</div>

		<hr />

		<div class="div_box">

		</div>

	</div>
</template>

<script>
import { ref, reactive, computed } from 'vue'

export default {
	name: 'App',
	setup() {
		let xLanguage = ref(99); // 切记要引用ref
		let xMaths = ref(120);
		let xEnglish = ref(38);

		let person = reactive({ // 切记要引用reactive
			firstName: '张',
			lastName: '三',
		})
		function changeEnglishScore() {
			xEnglish.value = 100; // 使用ref修改的时候，需要使用value
		}

		function changeUserName() {
			person.firstName = '李';
			person.lastName = '四';
		}

		// computed简写形式(⚠️记得引用computed)
		// person.fullName = computed(() => {
		// 	return person.firstName + '-' + person.lastName
		// })

		// computed非简写模式(⚠️记得引用computed)
		person.fullName = computed({
			get() {
				return person.firstName + '-' + person.lastName
			},
			set(value) {
				let nameArr = value.split('-')
				person.firstName = nameArr[0]
				person.lastName = nameArr[1]
			}
		})

		// 切记一点要return出去
		return {
			xLanguage,
			xMaths,
			xEnglish,
			changeUserName,
			changeEnglishScore,
			person
		}
	}
}
</script>

<style lang="less" scoped>
.app {
	background-color: #f5f5f5;
	border-radius: 10px;
	padding: 10px;

	button {
		margin-top: 8px;
		width: 200px;
	}

	.div_box {
		display: flex;
		flex-direction: column;
	}

}
</style>
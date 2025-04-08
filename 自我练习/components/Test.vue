<template>
	<div class="app">
		<div>{{ abc }}</div>
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
			<!-- 
			监视reactive所定义的一个响应式数据的全部属性
					1.注意：此处无法正确的获取oldValue
					2.注意：强制开启了深度监视（deep配置无效）
			-->
			<h4>3、学习vue3的监听属性</h4>
			<ul>
				<li>province: <a href="https://www.baidu.com/s?wd=北京市" target="_blank">{{
					address.province }}</a></li>
				<li>city: {{ address.city }}</li>
				<li>street: {{ address.street }}</li>
				<li v-if="isShow">c: {{ address.a.b.c }}</li>
			</ul>
			<button @click="address.street += '~'">修改street的值</button>
			<button @click="isShow = !isShow">显示/隐藏c的内容</button>
			<button @click="address.a.b.c += '。'">修改c的值</button>
		</div>

		<hr />

		<div class="div_box">
			<h4>4、学习vue3的hook函数(其实就是封装功能供大家直接使用)</h4>
			<span>当前点击时鼠标的坐标为：x：{{ point.x }}，y：{{ point.y }}</span>
		</div>

		<hr />

		<div class="div_box">
			<h4>5、var、let和const</h4>
			<span>①、var：由于 var 存在函数作用域和变量提升，在现代 JavaScript 开发中使用较少。不过，在一些旧代码或者需要兼容旧环境的场景中可能会用到。</span>
			<span>②、let：适用于需要在块级作用域中声明变量，并且可能会重新赋值的情况，例如在 for 循环中。</span>
			<span>③、const：适用于声明常量，一旦赋值就不希望被修改的情况。推荐在声明变量时优先考虑使用 const，只有当需要重新赋值时才使用 let。</span>
		</div>

		<hr />

		<div class="div_box">

		</div>

	</div>
</template>

<script>
import { ref, reactive, computed, watch } from 'vue'
import usePoint from '../hooks/usePoint'

export default {
	name: 'Test',
	props: ['abc'],
	setup() {
		let isShow = ref(false);
		let xLanguage = ref(99); // 切记要引用ref
		let xMaths = ref(120);
		let xEnglish = ref(38);
		let person = reactive({ // 切记要引用reactive
			firstName: '张',
			lastName: '三',
		})
		let address = reactive({
			province: '北京市',
			city: '海淀区',
			street: '西二旗',
			a: {
				b: {
					c: 100
				}
			}
		})
		let point = usePoint();

		function changeEnglishScore() {
			xEnglish.value = 100; // 使用ref修改的时候，需要使用value
		}

		function changeUserName() {
			person.firstName = '李'; // 使用reactive修改的时候，不需要使用value
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

		// watch(address, (newValue, oldValue) => {
		// 	console.log('⚠️测试打印的内容:--->', newValue, oldValue);
		// },{immediate:true})

		watch(() => address.a, (newValue, oldValue) => {
			console.log('⚠️测试打印的内容:--->', newValue, oldValue);
		}, { deep: true })

		let xxx = 100;
		console.log('xxx:', xxx);
		xxx = 200;//如果使用const声明xxx,则会报错
		console.log('xxx:', xxx);

		// 切记一点要return出去
		return {
			isShow,
			xLanguage,
			xMaths,
			xEnglish,
			changeUserName,
			changeEnglishScore,
			person,
			address,
			point
		}
	},
	beforeCreate() {
		console.log('---beforeCreate---')
	},
	created() {
		console.log('---created---')
	},
	beforeMount() {
		console.log('---beforeMount---')
	},
	mounted() {
		console.log('---mounted---')
	},
	beforeUpdate() {
		console.log('---beforeUpdate---')
	},
	updated() {
		console.log('---updated---')
	},
	beforeUnmount() {
		console.log('---beforeUnmount---')
	},
	unmounted() {
		console.log('---unmounted---')
	},
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

	li {
		border-bottom: 2px solid red;
	}
}
</style>
<template>
	<Test :abc="xxx" />
	<br />
	<CustomRef />
</template>

<script>
import { ref } from 'vue'
import Test from './components/Test.vue'
import CustomRef from './components/CustomRef.vue';
export default {
	name: 'App',
	components: {
		Test,
		CustomRef
	},
	setup() {
		let xxx = ref('我是App组件的xxx')
		return {
			xxx,
		}
	}
}
</script>
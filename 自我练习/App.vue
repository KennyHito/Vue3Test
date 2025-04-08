<template>
	<Test />
	<br />
	<CustomRef />
</template>

<script>
import Test from './components/Test.vue'
import CustomRef from './components/CustomRef.vue';
export default {
	name: 'App',
	components: {
		Test,
		CustomRef
	}
}
</script>
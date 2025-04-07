<template>
	<h2>我是Test组件</h2>
	<h2>当前点击时鼠标的坐标为：x：{{ point.x }}，y：{{ point.y }}</h2>
</template>

<script>
import { onMounted } from 'vue'
import usePoint from '../hooks/usePoint'
export default {
	name: 'Test',
	setup() {
		const point = usePoint()
		onMounted(() => {
			console.log('⚠️测试打印的内容:--->', 'Test');
		})
		return { point }
	}
}
</script>
<template>
	<h1>一个人的信息</h1>
	<h2>姓名：{{name}}</h2>
	<h2>年龄：{{age}}</h2>
	<h3>工作种类：{{job.type}}</h3>
	<h3>工作薪水：{{job.salary}}</h3>
	<h3>写了{{job.content.code}}行代码</h3>
	<h3>爱好:</h3>
	<ul>
		<li v-for="item in hobby" :key="item">{{item}}</li>
	</ul>
	<h3>办公地点:</h3>
	<ul>
		<li>{{address.province}}{{address.city}}{{address.county}}{{address.detail}}</li>
	</ul>

	<button @click="changeInfo">修改人的信息</button>
</template>

<script>
	import {ref} from 'vue'
	export default {
		name: 'App',
		setup(){
			//数据
			let name = ref('张三')
			let age = ref(18)
			let job = ref({
				type:'前端工程师',
				salary:'30K',
				content:{
					code:98302,
				}
			})
			let hobby = ref(['抽烟','喝酒','烫头'])
			let address = ref({
				province:'北京',
				city:'北京',
				county:'朝阳区',
				detail:'中建财富国际中心'
			})

			//方法
			function changeInfo(){
				name.value = '李四'
				age.value = 48
				console.log(name,age)
			
				job.value.type = 'java后端'
				job.value.salary = '60K'
				job.value.content.code = 99999
				console.log(job.value)

				hobby.value[0] = '学习'
				hobby.value[2] = '打羽毛球'
				console.log(hobby.value)

				address.value.county = '海淀区'
				address.value.detail = '西二旗'
				console.log(address.value)
			}

			//返回一个对象（常用）
			return {
				name,
				age,
				job,
				hobby,
				address,
				changeInfo
			}
		}
	}
</script>


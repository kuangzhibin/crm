<template>
	<div class="navMenu">
		<el-row class="tac">
			<el-col :span="24">
				<el-menu class="el-menu-vertical-demo" @select='handleSelect' :default-active='this.activeName'>
					<el-submenu index="1">
						<template slot="title"><span class="icon iconfont icon-dashboard"></span> 销售部门日常工作</template>
						<el-menu-item index="客户管理:1">客户管理</el-menu-item>
					</el-submenu>
					<el-submenu index="2">
						<template slot="title"><span class="icon iconfont icon-iconbriefcase"></span> 市场客户管理</template>
						<el-menu-item index="新增客户:1">新增客户</el-menu-item>
						<el-menu-item index="跟进中客户:1">跟进中客户</el-menu-item>

						<el-submenu index='2-3'>
							<template slot="title">客户管理</template>
							<el-menu-item index="客户管理:2">客户管理</el-menu-item>
							<el-menu-item index="检查重复客户:1">检查重复客户</el-menu-item>
							<el-menu-item index="停TURN:1">停TURN</el-menu-item>
						</el-submenu>

						<el-menu-item index="预约到访查询:1">预约到访查询</el-menu-item>
						<el-menu-item index="分配客户:1">分配客户</el-menu-item>
						<el-menu-item index="公海客户管理:1">公海客户管理</el-menu-item>
						<el-menu-item index="活动管理:1">活动管理</el-menu-item>
						<el-menu-item index="关怀管理:1">关怀管理</el-menu-item>

					</el-submenu>
					<el-submenu index="3">
						<template slot="title"><span class="icon iconfont icon-sitemap"></span> 校区客户管理</template>

						<el-menu-item index="新增客户:2">新增客户</el-menu-item>
						<el-menu-item index="预约到访客户:1">预约到访客户</el-menu-item>
						<el-menu-item index="跟进中客户:2">跟进中客户</el-menu-item>

						<el-submenu index='3-4'>
							<template slot="title">客户管理</template>
							<el-menu-item index="客户管理:3">客户管理</el-menu-item>
							<el-menu-item index="检查重复客户:2">检查重复客户</el-menu-item>
							<el-menu-item index="停TURN:2">停TURN</el-menu-item>
						</el-submenu>
						<el-menu-item index="分配客户:2">分配客户</el-menu-item>
						<el-menu-item index="关怀管理:2">关怀管理</el-menu-item>

					</el-submenu>
					<el-submenu index="4">
						<template slot="title"><span class="icon iconfont icon-cogs"></span> 系统管理</template>
						<el-menu-item index="权限设置:1">权限设置</el-menu-item>
						<el-menu-item index="规则设置:1">规则设置</el-menu-item>
					</el-submenu>

				</el-menu>

			</el-col>

		</el-row>

	</div>

</template>
<script>
	//引入组件
	import Hello from './Hello'
	import User from './User'


	export default {
		name: 'Navmenu',
		components: {},
		props: ['activeName'],
		data() {
			return {
				
				
			}
		},

		methods: {

			handleSelect(key, keyPath) {
				this.$emit('handleSelect', key);

			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
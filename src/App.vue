<template>
	<div id="app">

		<div class="logo">
			<span class="only_title icon iconfont icon-onlyicon"> 昂立CRM 0.1</span>
			
			
			<div class="right login">
				<el-dropdown class="login">
					<el-button type="primary">
						<img class="userPhoto" src="./assets/like1.jpg" /> 登录用户<i class="el-icon-caret-bottom el-icon--right"></i>
					</el-button>   
					<el-dropdown-menu slot="dropdown">
						<el-dropdown-item class="el-icon-setting"> 退出登录</el-dropdown-item>

					</el-dropdown-menu>
				</el-dropdown>
			</div>
		</div>

		<div id="main" class="">
					<!--左侧导航菜单-->
					<div id="navMenu" class="">
						<Navmenu v-on:handleSelect="addTabnav"></Navmenu>
					</div>
			 <!--右侧tab切换-->
					<div id="navTab" class="">
		
						<el-tabs type="card" v-bind:active-name="activeTab">
							<el-tab-pane name="firsticon">
								<span slot="label"><i class="icon iconfont icon-dashboard"></i></span>
							</el-tab-pane>
							<el-tab-pane closable v-for="(item, index) in tabs" :label="item.title" :name="item.name" >
								<component :is="item.content"></component>
							</el-tab-pane>
						</el-tabs>
		
					</div>
			
			
		</div>

	</div>

</template>
<script>
	import Navmenu from './components/Navmenu' //导航菜单
	import Newcreateuser from './components/Newcreateuser'  //新增客户
	import Hello from './components/Hello'  //测试
	import User from './components/User'   //测试



//导航菜单menu-item与tabnav映射{'index:x':'对应的组件名称'}-----x位用于区分同名菜单项
	var menuList = {
		'客户管理:': 'User',
		'跟进中客户:': 'User',
		'权限设置:': 'Hello',
		'新增客户:':'Newcreateuser',
		'新增客户:2':'User'
	}
	
	
	export default {
		name: 'app',
		data() {
			return {
				tabs: [],
				menu: menuList,
				activeTab:'firsticon'

			}
		},
		components: {
			Navmenu,
			Hello,
			User,
			Newcreateuser
		},
		methods: {

			addTabnav(key) {
//			console.log("已经选择" + key);
			  var _name=key.split(":")[0];
			 for(var k in this.tabs){
			 	if(key==this.tabs[k].onlykey){
			 		console.log(this.tabs[k].onlykey)
			 		return;
			 	}
			 }
			
				this.tabs.push({
					name: _name,
					title: _name,
					onlykey:key,
					content: this.menu[key]
				});
				this.activeTab=_name;
				
			},
			disNavmenu(){
				console.log("你好")
			}
		}

	}
</script>

<style>
	/*公共样式*/
	
	body {
	
		font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
	}
	
	html,body,ul,li,ol,dl,dd,dt,p,h1,h2,h3,h4,h5,h6,form,fieldset,legend,img {margin: 0;padding: 0;}
	li {list-style: none;}
	a {text-decoration: none;}
	img {vertical-align: middle;}
	a img,fieldset {border: 0;}
	input,textarea,select {outline: none;}
	textarea {resize: none;}
	.left {	float: left;}
	.right {	float: right;}
	.cu-hand {cursor: pointer;}
  .clear {zoom: 1;}
	.clear:after {content: "";clear: both;display: block;height: 0;overflow: hidden;visibility: hidden;}
	
	
	
	/**/
	
	html,
	body {
		width: 100%;
		height: 100%;
	}
	

	
	#app {
		height: 100%;
		position: relative;
	}
	
	#app .logo {
		background: #4cb479;
		height: 44px;
		color: #fff;
		padding-left: 20px;
	}
	
	#app .logo .icon {
		font: 22px/44px "";
	}
	
	#app .logo .login button {
		height: 40px;
		background: #4cb479;
		border-color: #4cb479;
		padding: 4px;
	}
	#app .logo .login .userPhoto{
		width: 35px;
		height: 35px;
		border-radius: 50%;
	}
	#main {
		height: 100%;
		display: flex;
	}
	#main .el-row.tac,.el-col{
		height: 100%;
	}
	#navMenu {
		color: #4cb479;
		width: 300px;
		height: 1000px;
		position: relative;
		border: 1px solid #CCC;
		border-width: 0 1px 0 0;
		background-color: #F2F2F2;
		padding-left: 10px;
	}
	
	#navTab {
		width: 100%;
		height: 980px;
		padding: 10px 15px;
	}
	
	#navTab .el-tabs {
		height: 100%;
	}
	/**/
	
	.el-menu {
		background-color: #F2F2F2;
	}
	
	.el-submenu .el-menu {
		background-color: #F2F2F2;
	}
	
	.el-tabs__header {
		margin: 0;
	}
	
	.el-tabs--card .el-tabs__item {
		border: 1px solid #c5d0dc;
		border-left: 0;
		background: #f9f9f9;
	}
	
	.el-tabs__header:nth-child(1) {
		border-left: 1px solid #c5d0dc;
	}
	
	.el-tabs--card .el-tabs__item.is-active {
		border-top: 2px solid #4db97b;
		border-bottom: 0;
		background: #fff;
		color: #4db97b;
		border-left: 0;
	}
	
	.el-tabs__content {
		height: 908px;
		border: 1px solid #c5d0dc;
		border-top: 0;
		padding: 20px;
	}
</style>
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
						<Navmenu v-on:handleSelect="addTabnav" :activeName="this.activeTab"></Navmenu>
					</div>
			 <!--右侧tab切换-->
					<div id="navTab" class="">
            <NavTab :activeTab="this.activeTab" :tabs="this.tabs" @isClick="handleClick" @isRemove="handleRemove"></NavTab>


          </div>


		</div>

	</div>

</template>
<script>
	import Navmenu from './components/Navmenu' //导航菜单
  import NavTab from './components/NavTab'


//导航菜单menu-item与tabnav映射{'index:x':'对应的组件名称'}-----x位用于区分同名菜单项
	var menuList = {
		'客户管理:1': 'User',
		'新增客户:1:': 'User',
		'跟进中客户:1': 'Hello',
		'客户管理:2':'Newcreateuser',
		'检查重复客户:1':'',
		'停TURN:1':'',
		'预约到访查询:1':'',
		'分配客户:1':'',
		'公海客户管理:1':'',
		'活动管理:1':'Activty',
		'关怀管理:1':'ActivtyItem',
		'新增客户:2':'',
		'预约到访客户:1':'',
		'跟进中客户:2':'',
		'客户管理:3':'',
		'检查重复客户:2':'',
		'停TURN:2':'',
		'分配客户:2':'',
		'关怀管理:2':'',
		'权限设置:1':'',
		'规则设置:1':''
	}


	export default {
		name: 'app',
		data() {
			return {
				tabs: [{
          name:'firsticon',
          title:'',
          content:'',
          only:true
        }],
				menu: menuList,
				activeTab:'firsticon',
				activeMenu:''

			}
		},
		components: {
			Navmenu,
      NavTab
		},
		methods: {

			addTabnav(key) {
	//			console.log("已经选择" + key);
			  	var _name=key.split(":")[0];
				for(var k in this.tabs){
				 	if(key==this.tabs[k].onlykey){
//				 		console.log(this.tabs[k].onlykey)
            this.activeTab = key
            this.activeMenu = key
				 		return;
				 	}
				}

				this.tabs.push({
					name: key,
					title: _name,
					onlykey:key,
					content: this.menu[key]
				});
				this.activeTab=key;
			},
			disNavmenu(){
				console.log("你好")
			},
			handleClick(name){
//				console.log("xuanzhong"+tab, event.target.innerText)
//				console.log("xuanzhong"+tab, event)
				this.activeTab=name  //唯一与要改变的值  获取当前的index

			},
      handleRemove(tab){
        console.log(tab.name)
       this.tabs = this.tabs.filter(function(item){
          return item.name !== tab.name
        })
       //  console.log(this.tabs[this.tabs.length-1].name)
      }
			// handleRemove(tab){

			// 	this.tabs = this.tabs.filter(function(item){
   //        return item.name !== tab.name
   //      })
   //      console.log(this.tabs[this.tabs.length-1].name)
			// }
			// handleRemove(tab){
			// 	//this.tabs中删除当前的标签,改变activeMenu
      //   event.stopPropagation()
      //  event.preventDefault()
			// 	var _this=this;
			// 	for(var k in _this.tabs){
      //
			// 	 	if(tab.name==_this.tabs[k].name){
      //
			// 	 		console.log('删除'+k)
			// 			_this.tabs.splice(k,1);
			// 			if(k>0){
			// 				_this.activeTab=_this.tabs[k-1].name;
			// 				_this.activeMenu=_this.tabs[k-1].name;
			// 			}else{
			// 				_this.activeTab='firsticon';
			// 				_this.activeMenu='';
			// 			}
      //
      //
			// 	 	}
			// 	}
			// }
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

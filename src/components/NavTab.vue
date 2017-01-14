<template>
  <el-tabs type="card" :value="activeTab" @tab-click="handleClick" @tab-remove="handleRemove">
    <!--<el-tab-pane name="firsticon">
      <span slot="label"><i class="icon iconfont icon-dashboard"></i></span>
    </el-tab-pane>-->
    <el-tab-pane :closable="item.only?false : true" v-for="(item, index) in tabs" :label="item.title" :name="item.name" >
      <span v-if="item.only"  slot="label"><i class="icon iconfont icon-dashboard"></i>{{item.title}}</span>
      <component :is="item.content"></component>
    </el-tab-pane>
  </el-tabs>
</template>

<script>
  import Newcreateuser from './Newcreateuser'  //新增客户
  import Hello from './Hello'  //测试
  import User from './User'   //测试
  import Activty from './Activty'
  import ActivtyItem from './ActivtyItem'

  export default{
    data () {
      return {

      }
    },
    components: {
      Hello,
      User,
      Newcreateuser,
      Activty,
      ActivtyItem
    },
    props: ['activeTab', 'tabs'],
    methods: {
      handleClick(tab, event) {
        console.log(event);
        this.$emit('isClick', tab.name)
      },
      handleRemove(tab) {
        console.log("222")
        this.$emit('isRemove', tab)
      }
    }
  }
</script>

<style>

</style>

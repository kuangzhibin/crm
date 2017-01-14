<template>
<div class="activty">
  <form class="activty-search">
    <el-input style="width: 230px" placeholder="请输入内容" v-model.tirm="activtySearch.object">
      <template slot="prepend">活动名称</template>
    </el-input>
    <el-button type="primary">查询 <i class="el-icon-search"></i></el-button>
    <el-button type="text" native-type="reset">清除已选属性 <i class="el-icon-close" style="font-size:10px"></i></el-button>
  </form>
  <div class="activty-toolBar">
    <el-button><i class="el-icon-plus"></i> 新增</el-button>
    <el-button><i class="el-icon-loading"></i> 刷新</el-button>
    <el-button @click="handleRemove"><i class="el-icon-delete"></i> 删除</el-button>
    <el-button><i class="el-icon-circle-check"></i> 启用</el-button>
    <el-button><i class="el-icon-circle-cross"></i> 停用</el-button>
  </div>
  <div class="activty-table">
    <el-table
    :data="tableData3"
    border
    stripe
    style="width: 100%"
    @selection-change="handleSelectionChange">
      <el-table-column
        type="selection"
        width="55">
      </el-table-column>
      <el-table-column
        label="活动主题"
        prop="object"
        show-overflow-tooltip>
      </el-table-column>
      <el-table-column
        prop="type"
        label="活动类型"
        show-overflow-tooltip>
      </el-table-column>
      <el-table-column
        prop="timeBegin"
        label="开始时间"
        width="140"
        >
      </el-table-column>
      <el-table-column
        prop="timeEnd"
        label="结束时间"
        width="140"
        >
      </el-table-column>
      <el-table-column
        prop="status"
        label="状态"
        width="140">
      </el-table-column>
      <el-table-column
        label="操作"
        width="140">
        <template scope="scope">
          <el-button
            type="text"
            @click="toggleDialog(scope.$index, scope.row)">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
  <div class="activty-footer">
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage"
      layout="prev, pager, next, total, jumper"
      :total="52">
    </el-pagination>
  </div>
  <el-dialog title="编辑基本信息" v-model="dialogVisible">
    <div class="activtyNew">
      <div class="activtuNew-container">
      <el-form ref="EditActivtyInfoForm" class="activtyNew-Info" :model="copyRow" label-position="right" label-width="100px">
        <el-row :gutter="20">
          <el-col :span="6">
            <el-form-item label="活动名称" prop="object">
              <el-input v-model="copyRow.object"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="6" :offset="6">
            <el-form-item label="活动编号" prop="id">
              <el-input :disabled="true" v-model="copyRow.id"></el-input>
            </el-form-item></el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="负责人" prop="leader">
              <el-select v-model="copyRow.leader" placeholder="请选择">
                <el-option
                  v-for="item in options.leader"
                  :label="item.label"
                  :value="item.value">
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="8" :offset="4">
            <el-form-item label="活动状态" prop="status">
              <el-select v-model="copyRow.status" placeholder="请选择">
                <el-option
                  v-for="item in options.status"
                  :label="item.label"
                  :value="item.value">
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="活动类型" prop="type">
              <el-select v-model="copyRow.type" placeholder="请选择">
                  <el-option
                    v-for="item in options.type"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </el-form-item>
          </el-col>
          <el-col :span="8" :offset="4">
            <el-form-item label="课程产品" prop="product">
              <el-select v-model="copyRow.product" placeholder="请选择">
                  <el-option
                    v-for="item in options.product"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="目标客户" prop="target">
              <el-select v-model="copyRow.target" placeholder="请选择">
                  <el-option
                    v-for="item in options.target"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="8" :offset="4">
            <el-form-item label="预算" prop="budget">
              <el-input v-model="copyRow.budget"></el-input>
            </el-form-item></el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="10" >
            <el-form-item label="预期活动时间" prop="time">
              <el-date-picker type="daterange" placeholder="选择日期" v-model="copyRow.time"
               :picker-options="pickerOptions" style="width: 100%;"></el-date-picker>
      </el-col>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="20" :ofset="2">
            <el-form-item label="活动描述" prop="detail">
              <el-input type="textarea" :autosize="{ minRows: 4, maxRows: 10}" v-model="copyRow.detail"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      </div>
      <div class="activtuNew-footer">
        <el-button type="primary">保存</el-button>
        <el-button @click="resetForm">重置</el-button>
      </div>
    </div>
    <span slot="footer" class="dialog-footer">
      <el-button @click="dialogVisible = false">取 消</el-button>
      <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
    </span>
  </el-dialog>
</div>

</template>

<script>
  export default {
    name: 'Activty',
    data (){
      return {
        copyRow: {
          object: '',  // 活动名称
          id: '',  // 活动编号
          leader: '',  // 负责人
          status: '', // 活动状态
          type: '',  // 活动类型
          product: '', // 课程产品
          target: '',  // 目标客户
          budget: '',  // 预算
          time: '',  // 活动时间
          detail: ''  // 活动描述
        },
        pickerOptions: {
          disabledDate(time) {
            return time.getTime() < Date.now() - 8.64e7
          }
        },
        options: {
          leader: [
            {
              value: '1',
              label: '沈肖波'
            },
            {
              value: '2',
              label: '王骅'
            },
            {
              value: '3',
              label: '郭玲'
            },
            {
              value: '4',
              label: '崔凯'
            }
          ],
          status: [
            {
              value: '1',
              label: '激活'
            },
            {
              value: '2',
              label: '禁止'
            },
            {
              value: '3',
              label: '计划中'
            },
            {
              value: '4',
              label: '完成'
            }
          ],
          type: [
            {
              value: '1',
              label: '校区广告'
            },
            {
              value: '2',
              label: '网络广告'
            },
            {
              value: '3',
              label: '电话营销'
            }
          ],
          target: [
            {
              value: '1',
              label: '初一'
            },
            {
              value: '2',
              label: '初二'
            },
            {
              value: '3',
              label: '初三'
            },
            {
              value: '4',
              label: '高一'
            },
            {
              value: '5',
              label: '高二'
            },
            {
              value: '6',
              label: '高三'
            }
          ]
        },

        currentPage: 1, //分页默认为第一页
        dialogVisible: false, //弹框默认隐藏
        activtySearch: {
          object: '',
          type: '',
          status: '',
          time: ''
        },
        tableData3: [{
          type: '校区广告',
          object: '2017开春新新事',
          status: '激活',
          timeBegin: '2016-05-03',
          timeEnd: '2016-05-08'
        },
        {
          type: '电话营销',
          object: '王小虎',
          status: '计划中',
          timeBegin: '2016-05-03',
          timeEnd: '2016-05-08'
        },
        {
          type: '网络广告',
          object: '昂立教育30周年庆',
          status: '完成',
          timeBegin: '2016-05-03',
          timeEnd: '2016-05-08'
        }],
        multipleSelection: []
      }
    },
    methods: {
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },
      handleEdit(index, row){
        console.log('index:'+ index +'; row:'+ JSON.stringify(row))  //JSON.stringify(row)
      },
      handleSizeChange() {

      },
      handleCurrentChange(){

      },
      toggleDialog(index, row){
        console.log(JSON.stringify(row))
        this.dialogVisible = !this.dialogVisible
        this.activtyNewInfo = Object.assign({}, this.activtyNewInfo, row)
        this.copyRow = Object.assign({}, this.copyRow, row)
      },
      resetForm() {
        console.log(JSON.stringify(this.activtyNewInfo))
        this.copyRow = Object.assign({}, this.activtyNewInfo)
      },
      handleRemove() {
        if(this.multipleSelection.length){
          console.log(JSON.stringify(this.multipleSelection))
          for(var item in this.multipleSelection){
            console.log(item)
          }
        }else{
          alert('至少选择一个活动。')
        }
      }
    }
  }
</script>

<style>
  .activty{
    -webkit-text-size-adjust: none;
  }
  .activty-search{
    padding: 12px;
    background-color: #efefef;
    margin-bottom: 24px;
  }
  .activty-toolBar{
    margin-bottom: 12px;
  }
  .activty-table{
    text-align: center;
  }
  .activty-table .el-table th {
    text-align: center;
  }
  .activty-footer{
    float: right;
    margin-top: 12px;
  }
</style>

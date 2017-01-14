<template>
<div class="activtyNew">
  <div class="activtuNew-container">
    <div class="activtuNew-header">
      基本信息
    </div>
    <el-form ref="ActivtyInfoForm" class="activtyNew-Info" :model="activtyNewInfo" label-position="right" label-width="100px">
      <el-row :gutter="20">
        <el-col :span="6">
          <el-form-item label="活动名称" prop="name">
            <el-input v-model="activtyNewInfo.name"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6" :offset="6">
          <el-form-item label="活动编号" prop="id">
            <el-input :disabled="true" v-model="activtyNewInfo.id"></el-input>
          </el-form-item></el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="8">
          <el-form-item label="负责人" prop="leader">
            <el-select v-model="activtyNewInfo.leader" placeholder="请选择">
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
            <el-select v-model="activtyNewInfo.status" placeholder="请选择">
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
            <el-select v-model="activtyNewInfo.type" placeholder="请选择">
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
            <el-select v-model="activtyNewInfo.product" placeholder="请选择">
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
            <el-select v-model="activtyNewInfo.target" placeholder="请选择">
                <el-option
                  v-for="item in options.target"
                  :label="item.label"
                  :value="item.value">
                </el-option>
              </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="6" :offset="4">
          <el-form-item label="预算" prop="budget">
            <el-input v-model="activtyNewInfo.budget"></el-input>
          </el-form-item></el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="10" >
          <el-form-item label="预期活动时间" prop="time">
            <el-date-picker type="daterange" placeholder="选择日期" v-model="activtyNewInfo.time"
             :picker-options="pickerOptions" style="width: 100%;"></el-date-picker>
    </el-col>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="20" :ofset="2">
          <el-form-item label="活动描述" prop="detail">
            <el-input type="textarea" :autosize="{ minRows: 4, maxRows: 10}" v-model="activtyNewInfo.detail"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
  </div>
  <div class="activtuNew-footer">
      <el-button type="primary">保存</el-button>
      <el-button @click="resetForm('ActivtyInfoForm')">重置</el-button>
    </div>
</div>
</template>

<script>
  export default {
    data() {
      return {
        activtyNewInfo: {
          name: '',  // 活动名称
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
        // 日期选择器设置
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
        }
      }
    },
    methods: {
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    },
  }
</script>

<style>
  .activtuNew-container{
    border: 1px solid #eee;
    padding: 0 12px;
    margin-bottom: 26px;
  }
  .activtuNew-header{
    font-size: 20px;
    padding: 12px 0;
    border-bottom: 1px solid #eee;
  }
  .activtyNew-Info{
    padding: 16px;
  }
  .activtuNew-footer{
    text-align: center;
    margin-bottom: 12px;
  }
  .el-input{
    min-width: 220px;
  }
</style>

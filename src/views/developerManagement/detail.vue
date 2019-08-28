<template>
  <div class="app-container">
    <el-breadcrumb class="breadcrumb-marign">
      <el-breadcrumb-item :to="{ path: '/developerManagement/index' }">开发者管理</el-breadcrumb-item>
      <el-breadcrumb-item>开发者管理详情</el-breadcrumb-item>
    </el-breadcrumb>
    <el-row :gutter="20">
      <el-col :span="6"><div class="grid-content bg-purple">衣服/裤子/鞋/包</div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">护肤品/化妆品</div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">手机/充电宝/电脑</div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">小吃/零食</div></el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="6"><div class="grid-content bg-purple">衣服/裤子/鞋/包</div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">护肤品/化妆品</div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">手机/充电宝/电脑</div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">小吃/零食</div></el-col>
    </el-row>
    <el-card>想吃烤鱼，串串，火锅，烧烤，麻辣烫，臭豆腐，鸡爪，鸭掌，鸭脖，牛排，小龙虾，螃蟹，花甲，烤鱿鱼，酸菜鱼，鸡炖魔芋，鸡公煲，黄焖鸡，小面，米线，叫花鸡，辣子鸡，辣椒炒肉</el-card>
    <el-alert>头疼，想休息,duzonsndhou,vvyuuhunshennanshou,xuruo,chenyixia,nbfugn
      <el-row>tout</el-row>
    </el-alert>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
  <el-form-item label="活动名称" prop="name">
    <el-input v-model="ruleForm.name"></el-input>
  </el-form-item>
  <el-form-item label="活动区域" prop="region">
    <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>
  <el-form-item label="活动时间" required>
    <el-col :span="11">
      <el-form-item prop="date1">
        <el-date-picker type="date" placeholder="选择日期" v-model="ruleForm.date1" style="width: 100%;"></el-date-picker>
      </el-form-item>
    </el-col>
    <el-col class="line" :span="2">-</el-col>
    <el-col :span="11">
      <el-form-item prop="date2">
        <el-time-picker placeholder="选择时间" v-model="ruleForm.date2" style="width: 100%;"></el-time-picker>
      </el-form-item>
    </el-col>
  </el-form-item>
  <el-form-item label="即时配送" prop="delivery">
    <el-switch v-model="ruleForm.delivery"></el-switch>
  </el-form-item>
  <el-form-item label="活动性质" prop="type">
    <el-checkbox-group v-model="ruleForm.type">
      <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
      <el-checkbox label="地推活动" name="type"></el-checkbox>
      <el-checkbox label="线下主题活动" name="type"></el-checkbox>
      <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
    </el-checkbox-group>
  </el-form-item>
  <el-form-item label="特殊资源" prop="resource">
    <el-radio-group v-model="ruleForm.resource">
      <el-radio label="线上品牌商赞助"></el-radio>
      <el-radio label="线下场地免费"></el-radio>
    </el-radio-group>
  </el-form-item>
  <el-form-item label="活动形式" prop="desc">
    <el-input type="textarea" v-model="ruleForm.desc"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
    <el-button @click="resetForm('ruleForm')">重置</el-button>
  </el-form-item>
</el-form>
  </div>
</template>

<script>
console.log(window.location.href,'window.location.href', '好想暴富，没有钱','总是一时兴起')
export default {
  name: 'ComplexTable',
  data() {
    return {
      name: 'xq',
      url: window.location.href,
      id: window.location.href.split('detail/')[1],
      route: null,
      ruleForm: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      rules: {
        name: [
          { required: true, message: '请输入活动名称', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        region: [
          { required: true, message: '请选择活动区域', trigger: 'change' }
        ],
        date1: [
          { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
        ],
        date2: [
          { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
        ],
        type: [
          { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
        ],
        resource: [
          { required: true, message: '请选择活动资源', trigger: 'change' }
        ],
        desc: [
          { required: true, message: '请填写活动形式', trigger: 'blur' }
        ]
      }
    }
  },
  watch: {
    $route(route){
      console.log(route,'watch','ayzlzqsss')
      this.route=route
      return route
    }
  },
  methods: {
    submitForm(formName) {
      console.log(formName,'formName',this.ruleForm)
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
  }
}
</script>
<style>
  .breadcrumb-marign{
    margin-bottom: 20px;
  }
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    } 
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    text-align: center;
    line-height: 36px;
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>
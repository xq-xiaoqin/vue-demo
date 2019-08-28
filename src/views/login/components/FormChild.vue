<template>
  <div>
    <el-form :rules="rules" v-show="showAccount" :label-position="labelPosition" label-width="80px" :model="ruleForm" ref="ruleForm" :hide-required-asterisk="false">
      <el-form-item
        label="账号/手机号码/邮箱地址"
      >
        <el-input v-model="ruleForm.account"></el-input>
      </el-form-item>
      <el-form-item
        label="密码"
      >
        <el-input v-model="ruleForm.password"></el-input>
      </el-form-item>
      <el-form-item
        label="图形验证码"
      >
        <el-input v-model="ruleForm.captcha" class='captcha-input'>
        </el-input>
        <img :src='logo' class="captcha-img">
      </el-form-item>
      <el-form-item>
        <el-button type="primary" class="btn-width" @click="submitForm('ruleForm')">登录</el-button>
      </el-form-item>
    </el-form>

    <el-form v-show="showMsg" :inline="true" :model="formInline" class="demo-form-inline">
      <p>验证码已发送至{{mobile}}</p>
      <el-form-item
        :rules="[
          { required: true, message: '验证码不能为空'},
          { type: 'number', message: '验证码必须为数字值'}
        ]"
      >
        <el-input maxlength="1" v-model="formInline.code1" class="captcha-msg"></el-input>
      </el-form-item>
      <el-form-item
        :rules="[
          { required: true, message: '验证码不能为空'},
          { type: 'number', message: '验证码必须为数字值'}
        ]"
      >
        <el-input maxlength="1" v-model="formInline.code2" class="captcha-msg"></el-input>
      </el-form-item>
      <el-form-item
        :rules="[
          { required: true, message: '验证码不能为空'},
          { type: 'number', message: '验证码必须为数字值'}
        ]"
      >
        <el-input maxlength="1" v-model="formInline.code3" class="captcha-msg"></el-input>
      </el-form-item>
      <el-form-item
        :rules="[
          { required: true, message: '验证码不能为空'},
          { type: 'number', message: '验证码必须为数字值'}
        ]"
      >
        <el-input maxlength="1" v-model="formInline.code4" class="captcha-msg"></el-input>
      </el-form-item>
      <el-form-item
        :rules="[
          { required: true, message: '验证码不能为空'},
          { type: 'number', message: '验证码必须为数字值'}
        ]"
      >
        <el-input maxlength="1" v-model="formInline.code5" class="captcha-msg"></el-input>
      </el-form-item>
      <el-form-item
        :rules="[
          { required: true, message: '验证码不能为空'},
          { type: 'number', message: '验证码必须为数字值'}
        ]"
      >
        <el-input maxlength="1" v-model="formInline.code6" class="captcha-msg"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" class="btn-width" @click="submitForm('formInline')">登录</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
// import openWindow from '@/utils/open-window'

export default {
  name: 'FormChild',
  props: [
    'message',
    'labelPosition',
    'ruleForm',
    'rules',
    'logo',
    'formInline',
    'showAccount',
    'showMsg',
    'mobile'
    ],
  deta(){
  },
  methods: {
    submitForm(ruleForm) {
      console.log(ruleForm,'submit')
      this.$refs[ruleForm].validate((valid) => {
        console.log(valid,'valid')
        if (valid) {
          // alert('submit!');
          // this.loading = true
          this.$store.dispatch('user/login', this.ruleForm)
            .then(() => {
              this.$router.push({ path: this.redirect || '/', query: this.otherQuery })
              // this.loading = false
            })
            .catch(() => {
              console.log('loading')
              // this.loading = false
            })
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

<style lang="scss" scoped>

</style>

<template>
  <div class="login-container">
    <el-menu
      class="el-menu-demo"
      mode="horizontal"
      background-color="#fff"
      text-color="#333"
      active-text-color='#333'
    >
      <img src='../../assets/top-logo.png' class="top-img" />
      <el-menu-item index="2"><a href="https://it.open.10086.cn/#/home" target="_blank">首页</a></el-menu-item>
      <el-menu-item index="3"><a href="https://it.open.10086.cn/#/home" target="_blank">产品</a></el-menu-item>
      <el-menu-item index="4"><a href="https://it.open.10086.cn/#/home" target="_blank">解决方案</a></el-menu-item>
      <el-menu-item index="5"><a href="https://it.open.10086.cn/#/home" target="_blank">帮助文档</a></el-menu-item>
      <el-menu-item index="6"><a href="https://it.open.10086.cn/#/home" target="_blank">在线体验</a></el-menu-item>
      <el-button class='top-btn' type="primary" @click="this.reload">
        <svg-icon icon-class="reload" />
        开发平台
      </el-button>
    </el-menu>
    <el-card class="box-card">
      <el-tabs v-model="activeName" @tab-click="handleClick">
        <el-tab-pane label="账号登录" name="first">
          <el-form v-show="showAccount" :rules="rules" :label-position="labelPosition" label-width="80px" :model="ruleForm" ref="ruleForm" :hide-required-asterisk="false">
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
        </el-tab-pane>
        <el-tab-pane label="子账号登录" name="second">
          <child
            :labelPosition='labelPosition'
            :message='prentProps'
            :ruleForm='ruleForm'
            :rules='rules'
            :logo='logo'
            :formInline='formInline'
            :showAccount='showAccount'
            :showMsg='showMsg'
            :showImgCaptcha='showImgCaptcha'
            :mobile='mobile'
          >
          </child>
        </el-tab-pane>
      </el-tabs>
  </el-card>
  </div>
</template>

<script>
import child from './components/FormChild'
export default {
  name: 'Login',
  components: {
    child,
  },
  data() {
    return {
      activeName: 'first',
      prentProps: 'hello child',
      logo: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
      showAccount: true,
      showMsg: false,
      showImgCaptcha: false,
      mobile: '',
      labelPosition: 'top',
      ruleForm: {
        account: '',
        password: '',
        captcha: ''
      },
      formInline: {
        code1: '',
        code2: '',
        code3: '',
        code4: '',
        code5: '',
        code6: ''
      },
      rules: {
        account: [{ required: true, trigger: 'blur', message: '请选择活动资源'}],
        password: [{ required: true, trigger: 'blur',message: '请选择活动资源'}],
        captcha: [{ required: true, trigger: 'blur',message: '请选择活动资源'}],
      },
    }
  },
  watch: {
  },
  created() {
  },
  mounted() {
    // if (this.loginForm.username === '') {
    //   this.$refs.username.focus()
    // } else if (this.loginForm.password === '') {
    //   this.$refs.password.focus()
    // }
  },
  destroyed() {
    // window.removeEventListener('storage', this.afterQRScan)
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
    handleClick(tab, event) {
      console.log(tab, event);
    },
    reload(){
      this.$router.go(0);
    }
  }
}
</script>

<style lang="scss">
.login-container {
  width: 100%;
  height: 100%;
  overflow: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-image: url('../../assets/login-img.png'), url('../../assets/login--bg.png');
  background-repeat: no-repeat, no-repeat;
  background-position: 0px, 0px;
  background-size: cover;
  position: fixed;
  background-color: #272a3a;
  .el-menu-demo{
    height: 60px;
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 111;
  }
  .el-menu.el-menu--horizontal{
    border-bottom: none;
    .top-img{
      float: left;
      width: 260px;
      margin: 13px 10px 10px 31px;
    }
    .top-btn{
      float: right;
      margin-right: 10%;
      margin-top: 10px;
      color: #189fff;
      background-color: #fff
    }
  }
  .el-menu--horizontal > .el-menu-item.is-active{
    border-bottom: none
  }
  .box-card {
    z-index: 110;
    width: 400px;
    position: absolute;
    right: 10%;
    top: 15%;
    .el-card__body{
      padding: 16px 30px 30px;
    }
  }
  .el-input {
    display: inline-block;
    width: 100%;
    padding: 0;
  }
  .el-form-item{
    margin-bottom: 8px;
    .el-form-item__label{
      padding: 0;
      font-weight: 400;
    }
  }
  .el-tabs__item{
    font-size: 17px
  }
  .btn-width{
    width: 100%;
    margin-top: 20px;
  }
  .captcha-input{
    width: 50%;
    position: relative;
  }
  .captcha-img{
    position: absolute;
    right: 0;
    width: 40%;
    height: 36px;
  }
  .captcha-msg{
    width: 40px;
  }
}

</style>

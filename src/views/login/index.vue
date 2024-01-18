<template>
  <div class="login-container">
    <div class="logo" />
    <div class="form">
      <div class="deng">
        <h1>手机号登陆</h1>
        <el-form
          ref="ruleForm"
          :model="ruleForm"
          :rules="rules"
          class="demo-ruleForm"
        >
          <el-form-item prop="mobile">
            <el-input v-model="ruleForm.mobile" />
          </el-form-item>
          <el-form-item prop="password">
            <el-input v-model="ruleForm.password" show-password />
          </el-form-item>
          <el-form-item prop="isAgree">
            <el-checkbox v-model="ruleForm.isAgree">用户平台使用协议</el-checkbox>
          </el-form-item>
          <el-form-item>
            <el-button
              type="primary"
              style="width: 500px"
              @click="submitForm('ruleForm')"
            >登录</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ruleForm: {
        mobile: '',
        password: '',
        isArray: false
      },
      rules: {
        mobile: [
          { required: true, message: '请输入手机号', trigger: 'blur' },
          {
            pattern: /^1[3-9]\d{9}/,
            message: '手机号格式不正确',
            trigger: 'blur'
          }
        ],
        password: [
          { required: true, message: '请输入手机号', trigger: 'blur' },
          { min: 6, max: 16, message: '密码格式不正确', trigger: 'blur' }
        ],
        isAgree: [
          {
            validator: (rule, value, callback) => {
              // 当前的规则
              // value 当前v-mode所绑定的值
              // callback之必须要执行的函数  promise resove reject
              // callback()
              // callback(new Error("您当前的规则"))
              // rule规则
              // value检查的数据 true/false
              // callback 函数 执行这个函数
              // 成功执行callback 失败也执行callback(错误对象 new Error(错误信息))
              value ? callback() : callback(new Error('没有勾选用户平台协议'))
            }
          }
        ]
      }
    }
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.login-container {
  display: flex;
  justify-content: space-between;
  height: 100vh;
  .logo {
    flex: 3;
    background: rgba(38, 72, 16) url(../../assets/common/login_back.png);
    border-top-right-radius: 60px;
  }
  .form {
    flex: 2;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .deng {
    width: 500px;
  }
}
</style>

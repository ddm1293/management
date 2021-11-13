<template>
  <div style="width: 100%; height: 100vh; background-color: darkblue; overflow: hidden">
    <div style="width: 400px; margin: 150px auto">
      <div style="color: #cccccc; font-size: 30px; text-align: center; padding: 30px 0">欢迎注册</div>

      <el-form ref="form" :model="form" size="normal" :rules="rules">
        <el-form-item prop="username">
          <el-input v-model="form.username"
                    placeholder="请输入用户名"
                    :prefix-icon="User"
                    clearable>
          </el-input>
        </el-form-item>

        <el-form-item prop="password">
          <el-input v-model="form.password"
                    placeholder="请输入密码"
                    :prefix-icon="Lock"
                    show-password>

          </el-input>
        </el-form-item>

        <el-form-item prop="confirm">
          <el-input v-model="form.confirm"
                    placeholder="请再次输入密码"
                    :prefix-icon="Lock"
                    show-password>

          </el-input>
        </el-form-item>

        <el-form-item>
          <el-button style="width: 100%" type="primary" @click="register">注 册</el-button>
        </el-form-item>
      </el-form>

    </div>
  </div>
</template>

<script>
import { User, Lock } from '@element-plus/icons'
import request from "@/utils/request";

export default {
  name: "Register",
  data() {
    return {
      form: {},
      User,
      Lock,
      rules: {
        username: [
          {
            required: true,
            message: '请输入用户名',
            trigger: 'blur',
          },
        ],
        password: [
          {
            required: true,
            message: '请输入密码',
            trigger: 'blur',
          }
        ],
        confirm: [
          {
            required: true,
            message: '请再次输入密码',
            trigger: 'blur',
          }
        ],
      },
    }
  },
  methods: {
    register() {
      if (this.form.password !== this.form.confirm) {
        this.$message({
          type: "error",
          message: "密码不一致"
        })
        return
      }

      this.$refs['form'].validate((valid) => {
        if (valid) {
          request.post("/user/register", this.form).then(res => {
            if (res.code === '0') {
              this.$message({
                type: "success",
                message: "注册成功"
              })
              this.$router.push("/login") // 页面跳转到登录界面
            } else {
              this.$message({
                type: "error",
                message: res.msg
              })
            }
          })
        }
      })
    }
  }
}
</script>

<style scoped>

</style>
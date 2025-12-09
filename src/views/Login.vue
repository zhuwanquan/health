<template>
  <div>
    <AuthForm ref="form" mode="login" @submit="handleLogin" />
    <p class="hint">没有账号？ <router-link to="/register">去注册</router-link></p>
  </div>
</template>

<script>
import AuthForm from '../components/AuthForm.vue'

export default {
  components: { AuthForm },
  methods: {
    handleLogin(payload) {
      const { username, password } = payload
      const users = JSON.parse(localStorage.getItem('users') || '{}')
      const user = users[username]
      if (!user) {
        this.$refs.form.setMessage('用户不存在')
        return
      }
      if (user.password !== password) {
        this.$refs.form.setMessage('密码错误')
        return
      }
      // 简单的登录标记
      localStorage.setItem('currentUser', username)
      this.$refs.form.setMessage('登录成功！')
      setTimeout(() => {
        this.$router.push('/')
      }, 700)
    },
  },
}
</script>

<style scoped>
.hint { margin-top: 1rem; }
</style>

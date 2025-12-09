<template>
  <div>
    <AuthForm ref="form" mode="register" @submit="handleRegister" />
    <p class="hint">已有账号？ <router-link to="/login">去登录</router-link></p>
  </div>
</template>

<script>
import AuthForm from '../components/AuthForm.vue'

export default {
  components: { AuthForm },
  methods: {
    handleRegister(payload) {
      const { username, password, password2 } = payload
      if (password !== password2) {
        this.$refs.form.setMessage('两次密码不一致')
        return
      }
      const users = JSON.parse(localStorage.getItem('users') || '{}')
      if (users[username]) {
        this.$refs.form.setMessage('用户名已存在')
        return
      }
      users[username] = { password }
      localStorage.setItem('users', JSON.stringify(users))
      this.$refs.form.setMessage('注册成功，正在跳转…')
      setTimeout(() => this.$router.push('/login'), 800)
    },
  },
}
</script>

<style scoped>
.hint { margin-top: 1rem; }
</style>

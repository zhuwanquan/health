<template>
  <div class="auth-card card">
    <h1>{{ title }}</h1>
    <form @submit.prevent="onSubmit">
      <div class="field">
        <label>用户名</label>
        <input v-model="form.username" required minlength="3" />
      </div>

      <div class="field">
        <label>密码</label>
        <input v-model="form.password" type="password" required minlength="6" />
      </div>

      <div v-if="mode === 'register'" class="field">
        <label>确认密码</label>
        <input v-model="form.password2" type="password" required minlength="6" />
      </div>

      <div class="actions">
        <button type="submit">{{ buttonText }}</button>
      </div>
    </form>
    <p class="meta" v-if="message">{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'AuthForm',
  props: {
    mode: { type: String, default: 'login' },
  },
  data() {
    return {
      form: { username: '', password: '', password2: '' },
      message: '',
    }
  },
  computed: {
    title() {
      return this.mode === 'register' ? '注册' : '登录'
    },
    buttonText() {
      return this.mode === 'register' ? '创建账号' : '登录'
    },
  },
  methods: {
    onSubmit() {
      this.message = ''
      this.$emit('submit', { ...this.form })
    },
    setMessage(msg) {
      this.message = msg
    },
  },
}
</script>

<style scoped>
.auth-card {
  max-width: 420px;
  margin: 2rem auto;
  text-align: left;
}
.field {
  margin-bottom: 1rem;
}
.field label {
  display: block;
  margin-bottom: 0.35rem;
  font-weight: 600;
}
.field input {
  width: 100%;
  padding: 0.6rem 0.75rem;
  border-radius: 8px;
  border: 1px solid #2b2b2b;
  background: transparent;
  color: inherit;
}
.actions { text-align: right; }
.meta { margin-top: 0.75rem; color: #ffcccb; }
</style>

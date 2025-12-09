<script setup>
import { ref } from 'vue'
</script>

<template>
  <div id="app-root">
    <header class="site-header">
      <nav>
        <router-link to="/login">登录</router-link>
        <router-link to="/register">注册</router-link>
      </nav>
    </header>

    <main>
      <router-view />
    </main>
  </div>
</template>

<style scoped>
.site-header { display:flex; justify-content:flex-end; gap:1rem; margin-bottom:1rem }
nav a { color: inherit; text-decoration: none; padding: 0.25rem 0.5rem }
nav a.router-link-active { border-bottom: 2px solid #646cff }
</style>

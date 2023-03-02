<template>
  <div class="home-view">
    <LoginForm />
  </div>
</template>

<script>
import LoginForm from '../components/LoginForm.vue'

export default {
  name: 'HomeView',
  components: {
    LoginForm,
  },
};
</script>

<style scoped>
.home-view {
  min-height: 100vh;
  display: flex;
  align-items: center;
}
</style>

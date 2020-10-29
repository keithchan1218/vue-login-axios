
<template>
  <div>
    <h1 v-if="e_name==''">Hi {{ username }}</h1>
    <h1 v-else >Hi {{ e_name }}</h1>
    <p>{{ secretMessage }}</p>
    <input type="button" value="Logout" @click="logout" />
  </div>
</template>

<script>
import AuthService from '@/services/AuthService.js';

export default {
  data() {
    return {
      secretMessage: '',
      username: '',
      e_name:''
    };
  },
  async created() {
    if (!this.$store.getters.isLoggedIn) {
      this.$router.push('/login');
    }

    this.username = this.$store.getters.getUser.username;
    this.e_name = this.$store.getters.getUser.e_name;

    this.secretMessage = await AuthService.getSecretContent();
  },
  methods: {
    logout() {
      this.$store.dispatch('logout');
      this.$router.push('/login');
    }
  }
};
</script>
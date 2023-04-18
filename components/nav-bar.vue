<template>
  <nav class="app-navbar m-chat-right m-project-bar">
    <nuxt-link class="login" tag="a" to="/login"
      >Login</nuxt-link
    >
    <p class="logout" @click="logout">Logout</p>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  },
  methods: {
    logout() {
        console.log(this.isAuthenticated, this.loggedInUser)
    //   try {
    //     await this.$axios.post('auth/logout')
    //   } catch (e) {
    //     //
    //   }
    }
  },
}
</script>

<style lang="scss">
.app-navbar {
  background: #fafafa;
  border: none;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.25);
  text-align: right;
  padding-right: 20px;
  height: 46px;
  position: fixed;
  width: 100%;
  z-index: 1001;
  display: flex;
  align-items: center;
  justify-content: flex-end;

  a.login {
    text-decoration: none;
    padding-right: 10px;
    color: black;
    font-weight: 700;
    font-size: 16px;
  }
  p.logout {
    text-decoration: none;
    padding-right: 10px;
    color: black;
    font-weight: 700;
    font-size: 16px;
    cursor: pointer;
  }
}
</style>
<template>
  <router-view v-on:completeLogin="completeLogin"
                v-on:logOut="logOut"
                v-on:otroevento="otroEvento">
  </router-view>
</template>

<script>


export default {
  name: 'App',
  methods: {
    completeLogin: function(args) {
      const {
        access,
        refresh,
        username
      } = args;
      localStorage.setItem('access_token', access);
      localStorage.setItem('refresh_token', refresh);
      localStorage.setItem('username', username);
      this.$router.push({
        name:"Home"
      });
    },
    logOut: function() {
      localStorage.removeItem('access_token');
      localStorage.removeItem('refresh_token');
      localStorage.removeItem('username');
      this.$router.push({
        name: 'logIn'
      })
    },
    otroEvento: function() {
      alert('captura evento de nieto');
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body{
   background: rgb(13, 38, 120, 0.2);
}
</style>

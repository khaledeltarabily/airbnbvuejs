<template>
  <div id="app">
    <div id="nav">
      <navbar msg="Welcome to Your Vue.js App"  />
    </div>
    <router-view />
  </div>
</template>


<script>
// @ is an alias to /src
import navbar from "@/components/navbar.vue";

export default {
  name: "home",
  components: {
    navbar
  }
};
</script>


<style lang="scss" scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
   
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

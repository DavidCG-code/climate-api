<template>
  <router-view />
</template>

<style lang="scss">
body {
  background-image: url("./assets/images/city.svg");
  background-repeat: no-repeat;
  background-size: 120%;
  background-position: -50px 105%;
  height: 100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: $colorSecondary;
    }
  }
}
</style>

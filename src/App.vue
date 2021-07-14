<template>
  <Navbar />
  <router-view />
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  components: { Navbar }
}
</script>

<style lang="scss">
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}

nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
  > a, button {
    flex-grow: 1;
    text-decoration: none;
    text-align: center;
    padding: 15px;
    border-radius: 8px;
    color: white;
    font-weight: 700;
    transition: all 0.2s linear;
  }
  > a {
    background-color: dodgerblue;
    &:hover, &.router-link-active {
      background-color: darken($color: dodgerblue, $amount: 20%);
    }
  }
}
</style>
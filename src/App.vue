<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import './assets/global.css'
</script>

<template>
  <div class="layout">
    <header class="center">
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/stone">stone</RouterLink>
      <RouterLink to="/raid-box">raid-box</RouterLink>
    </nav>
  </header>
  <main>
    <RouterView/>
  </main>
  </div>
  

</template>

<style scoped>

header {
  line-height: 1.5;
  height: 50px;
  background-color: slategray;
}

main{
  margin-top: 50px;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    position: absolute;
    top : 0;
    left:  0;
    display: flex;
    width: 100vw;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

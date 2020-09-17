<template>
  <div class="app">
    <div id="nav" hidden>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <img alt="Bookstore" src="./assets/bookstore.png" />
    <router-view/>
  </div>
</template>

<style>
div.app {
  text-align: center;
}
</style>

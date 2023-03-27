<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> <!--| <router-link to="/">Gallery</router-link>--> | <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style>
html, body {
    background-color: rgb(20, 20, 20);
    color: #ccc;
    margin: 0;
    padding: 0;
    height: 100%;
    width: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #ccc;
}

nav a.router-link-exact-active {
  color: #ce7b00;
}
</style>

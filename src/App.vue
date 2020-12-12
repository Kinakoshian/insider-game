<template>
  <div id="app">
    <h1>INSIDER GAME</h1>
    <router-view/>
  </div>
</template>

<style>
body {
  background-color: #f7f7f7;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
h1 {
  font-size: 32px;
  margin: 40px 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f79;
  text-align: center;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

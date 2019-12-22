<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
html {
  background: rgba(0, 0, 0, 0.1);
}

body {
  margin: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgba(0, 0, 0, 0.95);
}

[placeholder]:empty::before {
  content: attr(placeholder);
  display: block; /* For Firefox */
}

button,
input,
textarea {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 16px;
}
</style>

<template>
  <header>
    <h1>Your Website</h1>
  </header>

  <nav>
    <ul>
      <li>
        <router-link to="/home">Home </router-link>
      </li>
      <li>
        <router-link to="/home2">Home 2</router-link>
      </li>
    </ul>
  </nav>

  <main>
    <router-view :key="$route.path" />
  </main>

  <footer>
    <p>&copy; 2024 Your Website. All rights reserved.</p>
  </footer>
</template>

<script setup>
import Header from "../components/layout/header.vue";
import Footer from "../components/layout/footer.vue";
</script>

<style scoped>
@media (max-width: 700px) {
  .layout-main-bg {
    background: white;
  }
}
.layout-main-bg {
  min-height: 95vh;
  display: block;
  width: 100vw;
  /* flex-direction: column; */
}
.footer {
  margin-top: auto;
}
.main-content,
.header {
  z-index: 1;
}
body {
  font-family: "Arial", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

header {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 1em;
}

nav {
  background-color: #666;
  color: #fff;
  padding: 0.5em;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

nav li {
  display: inline;
  margin-right: 10px;
}

nav a {
  text-decoration: none;
  color: #fff;
}

main {
  padding: 20px;
}

footer {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 1em;
  position: fixed;
  bottom: 0;
  width: 100%;
}
</style>

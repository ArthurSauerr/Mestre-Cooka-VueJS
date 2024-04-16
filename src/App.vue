<template>
  <nav class="navbar">
    <div class="container">
      <div class="logo">
        <router-link to="/">
          <img class="cebola" alt="logo" src="./assets/logo-cebola.png" />
        </router-link>
      </div>
      <form @submit.prevent="submitSearch">
        <input v-model="search" placeholder="Procurar" class="search-bar" />
      </form>
      <ul class="nav-links">
        <router-link to="/">
          <li><a>Contato</a></li>
        </router-link>
        <router-link to="/about">
          <li><a>Sobre</a></li>
        </router-link>
      </ul>
    </div>
  </nav>
  <router-view />
</template>

<style>
body {
  background-color: #ebe2de;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #130c00;
  margin-top: 40px;
}
.search-bar {
  border: 2px solid #130c00;
  border-radius: 10px;
  padding: 8px;
  margin-left: 25%;
  font-size: 14px;
  font-weight: bold;
}
.navbar {
  background-color: #130c00;
  color: #fff;
  position: fixed; /* Define a posição fixa para a navbar */
  width: 100%;
  top: 0; /* Fixa a navbar no topo */
  left: 0;
  z-index: 1000; /* Define uma camada de sobreposição alta para a navbar */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2); /* Adiciona uma sombra */
}
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
}
.nav-links {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  margin-right: 5rem;
}
.nav-links li {
  margin-right: 1rem;
}
.nav-links li a {
  color: white;
  font-weight: bold;
  text-decoration: none;
  transition: color 0.3s;
}
.nav-links li a:hover {
  color: #ffc04c;
  border-bottom: 2px solid #ffc04c;
}
.cebola {
  width: 40px;
  margin-left: 5rem;
  transition: transform 0.3s ease;
}
.cebola:hover {
  transform: scale(1.2);
}
</style>

<!-- Navbar.vue -->

<template>
    <nav class="navbar">
      <div class="container">
        <div class="logo">
            <img class="cebola" alt="logo" src="../assets/logo-cebola.png">
        </div>
        <ul class="nav-links">
          <li><a href="#">Sobre</a></li>
          <li><a href="#">Contato</a></li>
        </ul>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    name: 'NavBar'
  }
  </script>
  
  <style>
  /* Estilos para a barra de navegação */
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
    margin-right: 5rem
  }
  .nav-links li {
    margin-right: 1rem;
  }
  .nav-links li a {
    color: white;
    font-weight: bold;
    text-decoration: none;
    transition: color .3s;
  }
  .nav-links li a:hover{
    color: #FFC04C;
    border-bottom: 2px solid #FFC04C;
  }
  .cebola{
    width: 40px;
    margin-left: 5rem;
    transition: all .3s;
  }
  .cebola:hover{
    width: 45px;
  }
  </style>
  
<template>
  <div>
    <header>
      <div class="bg-image"></div>
      <img id="logo" alt="logo" src="../assets/logo-cooka.png" />
      <h1>Bem-vindo(a), Mestre Cooka!</h1>
    </header>
    <h3>Acesse as melhores receitas abaixo!</h3>
    <div>
      <p>De qual lugar do mundo você quer encontrar receitas?</p>
      <button class="btn-tipo" @click="buscarReceitas('American')">EUA</button>
      <button class="btn-tipo" @click="buscarReceitas('Chinese')">China</button>
      <button class="btn-tipo" @click="buscarReceitas('French')">França</button>
      <button class="btn-tipo" @click="buscarReceitas('Japanese')">Japão</button>
    </div>
    <hr class="divider" />
    <div class="receitas-container" v-if="receitas.length > 0">
      <div class="receita" v-for="receita in receitas" :key="receita.idMeal">
        <img :src="receita.strMealThumb" :alt="receita.strMeal"/>
        <p>{{ receita.strMeal }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MestreCooka",
  props: {
    msg: String,
  },
  data() {
    return {
      receitas: [],
      erro: "",
    };
  },
  methods: {
    async buscarReceitas(country) {
      try {
        const response = await fetch(
          `https://www.themealdb.com/api/json/v1/1/filter.php?a=${country}`
        );
        if (response.ok) {
          const data = await response.json();
          this.receitas = data.meals;
        } else {
          throw new Error(`Erro ao buscar receitas: ${response.status}`);
        }
      } catch (error) {
        console.error("Ocorreu um erro ao buscar receitas:", error);
      }
    },
  },
};
</script>

<style scoped>
#logo {
  width: 22rem;
}
header {
  position: relative; /* Necessário para posicionar corretamente os elementos filhos */
  padding: 50px 0;
  text-align: center;
  overflow: hidden;
}
.bg-image {
  position: absolute; /* Posição absoluta para cobrir todo o header */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url("../assets/meal-bg.jpg");
  background-size: cover;
  background-position: center;
  transform: scaleX(1.1);
  filter: blur(5px);
  border-bottom: solid 5px #130c00;
  z-index: -1; 
  
}

.receitas-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.receita {
  text-align: center;
  width: calc(18% - 10px);
  margin: 10px;
}

.receita img {
  cursor: pointer;
  display: block;
  margin: 0 auto 10px;
  width: 12rem;
  border-radius: 10px;
  transition: transform 0.3s ease; /* Adiciona transição suave para o efeito de hover */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
}

.receita img:hover {
  transform: scale(
    1.1
  ); /* Aumenta a escala da imagem em 10% ao passar o mouse sobre ela */
}

h1 {
  font-size: 26px;
  font-family: Roobert, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  color: white;
}
p {
  font-weight: bold;
}
.divider {
  width: 87%;
  border: 1px solid #130c00;
}
.btn-tipo {
  appearance: none;
  background-color: transparent;
  border: 2px solid #130c00;
  border-radius: 15px;
  color: #130c00;
  cursor: pointer;
  font-family: Roobert, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  outline: none;
  padding: 16px 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(0.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 10%;
  will-change: transform;
  margin: 1rem;
}
.btn-tipo:disabled {
  pointer-events: none;
}
.btn-tipo:hover {
  color: #fff;
  background-color: #130c00;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}
.btn-tipo:active {
  box-shadow: none;
  transform: translateY(0);
}
</style>

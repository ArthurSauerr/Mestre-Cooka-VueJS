<template>
  <div>
    <h1>{{ msg }}</h1>
    <h3>Acesse as melhores receitas abaixo!</h3>
    <hr class="divider">
    <div>
      <p> De qual lugar do mundo você quer encontrar receitas? </p>
      <button class="btn-tipo" @click="buscarReceitas('American')"> EUA </button>
      <button class="btn-tipo" @click="buscarReceitas('Chinese')"> China </button>
      <button class="btn-tipo" @click="buscarReceitas('French')"> França </button> 
    </div>
    <!-- Lista de receitas -->
    <div class="receitas-container" v-if="receitas.length > 0">
      <div class="receita" v-for="receita in receitas" :key="receita.idMeal">
        <img :src="receita.strMealThumb" :alt="receita.strMeal" width="150">
        <p>{{ receita.strMeal }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MestreCooka',
  props: {
    msg: String
  },
  data() {
    return {
      receitas: [],
      erro: ''
    };
  },
  methods: {
    async buscarReceitas(tipo){
      try {
        // Fazer a requisição GET para a URL da API com base no tipo selecionado
        const response = await fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?a=${tipo}`);

        // Verificar se a resposta foi bem-sucedida (código de status 200)
        if (response.ok) {
          // Se for, converter a resposta para JSON
          const data = await response.json();
          this.receitas = data.meals;
        } else {
          // Se a resposta não for bem-sucedida, lançar um erro com o status da resposta
          throw new Error(`Erro ao buscar receitas: ${response.status}`);
        }
      } catch (error) {
        // Se ocorrer algum erro durante o processo, capturar e exibir no console
        console.error('Ocorreu um erro ao buscar receitas:', error);
      }
    }
  }
}
</script>

<style>
.receitas-container {
  display: flex;
  flex-wrap: wrap;
}

.receita {
  width: calc(33.33% - 20px); /* Ajuste conforme necessário */
  margin: 10px;
  text-align: center;
}

.receita img {
  cursor: pointer;
  display: block;
  margin: 0 auto 10px;
  border-radius: 10px;
  transition: transform 0.3s ease; /* Adiciona transição suave para o efeito de hover */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
}

.receita img:hover {
  transform: scale(1.1); /* Aumenta a escala da imagem em 10% ao passar o mouse sobre ela */
}

h1{
    font-size: 25px;
}
p{
    font-weight: bold;
}
.divider{
    width: 87%;
    border: 1px solid #130c00;
}
.btn-tipo {
  appearance: none;
  background-color: transparent;
  border: 2px solid #1A1A1A;
  border-radius: 15px;
  color: #3B3B3B;
  cursor: pointer;
  font-family: Roobert,-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  outline: none;
  padding: 16px 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
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
  background-color: #1A1A1A;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}
.btn-tipo:active {
  box-shadow: none;
  transform: translateY(0);
}
</style>
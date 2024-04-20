<template>
  <div>
    <h1>Resultado da Pesquisa {{ searchTerm }}</h1>
    <p v-if="receitas.length > 0">RECEITA: </p>
    <div class="receitas-container" v-if="receitas.length > 0">
      <div class="receita" v-for="receita in receitas" :key="receita.idMeal">
        <img :src="receita.strMealThumb" :alt="receita.strMeal"/>
        <p>{{ receita.strMeal }}</p>
      </div>
    </div>
    <p v-else>Nenhuma receita encontrada.</p>
  </div>
</template>

<script>
export default {
  props: {
    searchTerm: {
      type: String,
      required: true
    },
  },
  data() {
    return {
      receitas: []
    }
  },
  mounted(){
    this.submitSearch()
  },
  methods: {
    async submitSearch() {
      try {
        const response = await fetch(
          `https://www.themealdb.com/api/json/v1/1/search.php?s=${this.searchTerm}`
        );
        if (response.ok) {
          const data = await response.json();
          this.receitas = data.meals;
          console.log("Receita: ", data.meals)
        } else {
          throw new Error(`Erro ao buscar receita: ${response.status}`);
        }
      } catch (error) {
        console.log("Erro ao buscar receita: ", error)
      }
    }
  }
}
</script>
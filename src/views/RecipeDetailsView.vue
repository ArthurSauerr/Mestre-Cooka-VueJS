<template>
  <div>
    <h1>Resultado da Pesquisa</h1>
    <p v-if="receitas.length > 0"></p>
    <div class="receitas-container" v-if="receitas.length > 0">
      <div class="receita" v-for="receita in receitas" :key="receita.idMeal">
        <img :src="receita.strMealThumb" :alt="receita.strMeal"/>
        <p class="receita-title">{{ receita.strMeal }}</p>
        <p>Area: <br>{{ receita.strArea }}</p>
        <p>Type: <br>{{ receita.strCategory }}</p>
        <ul class="receita-list" v-if="receita.strIngredient1 !== null">
          <li v-for="ingredient in getIngredients(receita)" :key="ingredient">{{ ingredient }}</li>
        </ul>
        <!-- <hr class="divider"/> -->
        
      </div>
    </div>
    <p v-else>Buscando...</p>
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
    },
    getIngredients(receita) {
      const ingredients = [];
      for (let i = 1; i <= 20; i++) {
        const ingredientKey = `strIngredient${i}`;
        const measureKey = `strMeasure${i}`;
        if (receita[ingredientKey]) {
          ingredients.push(`${receita[ingredientKey]} - ${receita[measureKey]}`);
        } else {
          break;
        }
      }
      return ingredients;
    }
  }
}
</script>

<style scoped>
.receitas-container {
  display: flex;
  justify-content: center;
  margin-top: 80px;
}

.divider {
  width: 300%;
  margin-left: -100%;
  border: 1px solid #130c00;
}

.receita img{
  width: 300px;
  height: 300px;
  border-radius: 10px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
}

.receita-title{
  font-weight: bold;
  border-bottom: 2px solid #130c00;
}

.receita p{
  padding-top: 1px;
  font-weight: bold;
}
.receita-list{
  padding-top: 1px;
  font-weight: bold;
  align-items: left;
  text-align: left;
  margin-left: 50px;
}

</style>
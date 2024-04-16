<template>
    <div>
        <h1>{{ msg }}</h1>
        <h3>Acesse as melhores receitas abaixo!</h3>
        <hr class="divider">
        <div>
            <p> Que tipo de receita você quer fazer hoje? </p>
            <button class="btn-tipo"> Agridoce </button>
            <button class="btn-tipo"> Doce </button>
            <button class="btn-tipo"> Salgado </button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'MestreCooka',
  props: {
    msg: String
  }
}
</script>

<style>
h1{
    font-size: 25px;
}
p{
    font-weight: bold;
}
.divider{
    width: 87%;
    border: 1px solid #130c00; /* Cor e estilo da linha */
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

<template>
<div class="corpo">
  <h1 class="centralizado" >{{ titulo }}</h1>
  <ul>
    <li class="lista-fotos" v-for="foto in fotos">
      <meu-painel :titulo="foto.titulo">
        <img class="fotos imagem-responsiva" :src="foto.url"  :alt="foto.titulo"/>
      </meu-painel>
    </li>
  </ul>
</div>
</template>

<script>
import Painel from './components/shared/painel/Painel.vue'
export default {

  components: {
    'meu-painel': Painel
  },

  data() {
    return {
      titulo: "Lista de fotos",
      fotos: []
    }
  },
  created() {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
  
}
</script>

<style>
  .corpo{
    margin: 0 auto;
    font-family: Helvetica, sans-serif;
    width: 96%;
  }
  
  .centralizado{
    text-align: center;
  }

  .lista-fotos{
    display: inline-block;
  }

  .lista-fotos .fotos{
    list-style: none;
  }

  .imagem-responsiva {
    width: 100%;
  }
</style>

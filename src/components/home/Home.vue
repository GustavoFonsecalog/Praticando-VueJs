<template>
  <div>
    <h1 class="textCenter">{{titulo}}</h1>
    <input type="search" class="filter" @input="filtro= $event.target.value" placeholder="Filtre sua pesquisa">
    <ul class="listPic">
      <li class="picItem" v-for="(foto, idx) in filterPic" :key="idx">
        <meu-painel :titulo="foto.titulo">
          <respon-img :url="foto.url" :titulo="foto.titulo" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>

import Painel from '../shared/painel/Painel.vue';
import imagemResponsiva from '../shared/imagem-responsiva/imagemResponsiva.vue';

export default {

  components: {
    'meu-painel': Painel,
    'respon-img': imagemResponsiva

  },

  data() {

    return{
      titulo: 'Alurapic',
      fotos: [],
      filtro: ''     
    }

  },

  computed: {

    filterPic() {
        if(this.filtro){
        let expre = new RegExp(this.filtro.trim(), 'i')
        return this.fotos.filter(foto => expre.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

    created () {
      this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => alert("Erro"));
  },
}
  
</script>

<style>
  
  .textCenter {
    text-align: center;
  }

  .listPic {
    list-style: none;
  }

  .picItem {
    display: inline-block;
  }

  .filter {
    display: block;
    width: 100%;
  }

</style>

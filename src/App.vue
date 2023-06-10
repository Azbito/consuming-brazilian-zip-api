<script>
import axios from "axios";
import 'animate.css'

export default {

data() {
  return {
    info: null,
    cep: "84950-000"
  }
},  

  name: "getZipCode",

  async handleZip() {
   
  },

    methods: {
      onChange:function(event) {
        this.cep = event.target.value
      },
      handleZip:async function() {
         const {data} = await axios.get(`https://viacep.com.br/ws/${this.cep}/json/`)
         this.info = data
      }
    }

}
</script>

<template>
  <div class="search-container">
    <input @change="onChange($event)" @value="this.cep" placeholder="Digite um CEP" />
    <button @click="handleZip()">Procurar</button>
  </div>

  <div class="info-container animate__animated animate__fadeInUp" v-if="info">
      <p>CEP: <b>{{this.info.cep}}</b></p>
      <p>Localização: <b>{{this.info.localidade}}, <span>{{this.info.uf}}</span></b></p>
      <p>DDD: <b>({{this.info.ddd}})</b></p>
  </div>

</template>

<style lang="scss">
.search-container {
  margin-top: 5rem;
  gap: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  input {
    border: none;
    outline: none;
    padding: .5rem;
    border-radius: 10px
  }

  button {
    border: none;
    outline: none;
    padding: .5rem;
    border-radius: 16px;
    color: white;
    font-style: 700;
    font-family: "Poppins", sans-serif;
    cursor: pointer;
    background-color: rgb(45, 180, 140);

    transition: .2s;

    &:hover {
      background-color: rgb(70, 163, 135);
    }

    &:active {
      background-color: rgb(60, 141, 117);
    }
  }

}
  .info-container {
    background-color: rgb(114, 84, 196);
    padding: .5rem 2rem .5rem 2rem;
    border-radius: 16px;
    margin-top: 2rem;
    color: white
  }

</style>


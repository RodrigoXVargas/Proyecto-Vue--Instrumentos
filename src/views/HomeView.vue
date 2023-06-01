<template>
  <div class="Productos">
    <div class='grilla'>
      <div v-for="instrumento in instrumentosData" :key="instrumento.id">
        <CardInstrumento :instrumentoParam="instrumento" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import CardInstrumento from '@/components/CardInstrumento.vue';
import { defineComponent } from 'vue';
import { Instrumento } from '@/entidades/InstrumentoEntidad';


export default defineComponent({
  name: 'HomeView',
  components: {
    CardInstrumento
  },
  mounted(){
    this.getAllInstrumentos();
  },
  data(){
    return{
      instrumentosData: [] as Instrumento[]
    };
  },
  methods: {
    async getAllInstrumentos() {
      let urlServer = "http://localhost:8080/api/instrumentos/getAll";
      let response = await fetch(urlServer, {
          method: 'GET',
          headers: {
              'Content-type': "application/json",
              'Access-Control-Allow-Origin': '*'
          },
          mode: 'cors'
      });
      console.log(response);
      this.instrumentosData = await response.json();
    }
  }

});
</script>

<style>
.Productos {
  background-image: linear-gradient(to right, #42b983 -20%, #2c3e50 50%, #42b983 120%);
}

.grilla {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: 320px 300px;
    justify-items: center;
    grid-row-gap: 15px;
    padding: 20px 0px;
}


  

  
</style>

<template>
    <div class="DetalleView">
        <CardDetalle :instrumentoParam="instrumentoXid"/>
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import { Instrumento } from '@/entidades/InstrumentoEntidad';
import CardDetalle from '@/components/CardDetalle.vue';

export default defineComponent({
  name: 'DetalleView',
  components: {
    CardDetalle
  },
  mounted(){
    this.getInstrumentoById();
  },
  data(){
    return{
      instrumentoXid: {} as Instrumento
    };
  },
  methods: {
    async getInstrumentoById() {
        let parametroId = this.$route.params.id;
        let urlServer = "http://localhost:8080/api/instrumentos/get/"+parametroId;
        let response = await fetch(urlServer, {
            method: 'GET',
            headers: {
                'Content-type': "application/json",
                'Access-Control-Allow-Origin': '*'
            },
            mode: 'cors'
        });
        let resJson = await response.json();
        this.instrumentoXid = resJson;
        console.log(response);
}
  }
});
</script>

<style>
.DetalleView{
  background-image: linear-gradient(to right, #42b983 -20%, #2c3e50 50%, #42b983 120%);
}
</style>
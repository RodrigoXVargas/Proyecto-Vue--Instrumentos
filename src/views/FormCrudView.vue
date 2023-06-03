<template>
  <div isOpen={isOpen} onRequestClose={onClose} className='FormCrudPage'>
    <div className='form-container'>
      <h2>{{ instrumentoSeleccionado.id===0 ? 'Agregar instrumento' : 'Modificar instrumento' }}</h2>

      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Id</span>
        <input type="text" v-model="instrumentoSeleccionado.id" placeholder="Id" className="form-control" disabled
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Nombre</span>
        <input type="text" v-model="instrumentoSeleccionado.instrumento" placeholder="Nombre" className="form-control" required
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Marca</span>
        <input type="text" v-model="instrumentoSeleccionado.marca" placeholder="Marca" className="form-control" required
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Modelo</span>
        <input type="text" v-model="instrumentoSeleccionado.modelo" placeholder="Modelo" className="form-control" required
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Precio</span>
        <input type="text" v-model="instrumentoSeleccionado.precio" placeholder="Precio" className="form-control" required
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Costo de envio</span>
        <input type="text" v-model="instrumentoSeleccionado.costo_envio" placeholder="Costo de envio" className="form-control"  required
        aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Cantidad vendida</span>
        <input type="text" v-model="instrumentoSeleccionado.cantidad_vendida" placeholder="Cantidad vendida" className="form-control" required
        aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Path de la imagen</span>
        <input type="text" v-model="instrumentoSeleccionado.imagen" placeholder="Path de la imagen" className="form-control" required
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>
      <div className="input-group input-group-sm mb-3">
        <span className="input-group-text" id="inputGroup-sizing-sm">Descripcion</span>
        <input type="text" v-model="instrumentoSeleccionado.descripcion" placeholder="Descripcion" className="form-control" required
          aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" />
      </div>

      <div>
        <button type="submit" @click="saveInstrument(instrumentoSeleccionado)" className='btn btn-primary'>Guardar</button>
        <router-link :to="'/crud'"><button className='btn btn-secondary'>Atras</button></router-link>
      </div>

    </div>
  </div>
</template>
<script lang="ts">
import { Instrumento } from '@/entidades/InstrumentoEntidad';
import router from '@/router';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'FormCrudView',
  components: {},
  mounted() {
    this.getInstrumentoById();
  },
  setup() {
    const instrumentoSeleccionado = ref<Instrumento>(new Instrumento())
    return {
      instrumentoSeleccionado
    }
  },
  methods: {
    async getInstrumentoById() {
      let parametroId: string = this.$route.params.id as string;
      if (parseInt(parametroId) != 0) {
        let urlServer = "http://localhost:8080/api/instrumentos/get/" + parametroId;
        let response = await fetch(urlServer, {
          method: 'GET',
          headers: {
            'Content-type': "application/json",
            'Access-Control-Allow-Origin': '*'
          },
          mode: 'cors'
        });
        let resJson = await response.json();
        this.instrumentoSeleccionado = resJson;
        console.log(response);
      }
    },
    async saveInstrument(instrumento?: Instrumento) {
      let urlServer = 'http://localhost:8080/api/instrumentos/save';
      let methodM = "POST";
      if (instrumento && (instrumento.id) > 0) {
        urlServer = 'http://localhost:8080/api/instrumentos/update/' + instrumento.id;
        methodM = "PUT";
      }
      console.log(JSON.stringify(instrumento));
      await fetch(urlServer, {
        method: methodM,
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(instrumento),

      });
      router.push('/crud')
    }
  }
});

</script>
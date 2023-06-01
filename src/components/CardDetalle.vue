<template>
    <div class="Detalle">
        <div class="det-content">
            <div class="det-col1-content">
                <div class="imagen-content">
                    <img :src="getImageSource(instrumentoParam.imagen)" class="card-imagen" alt="imagen" />
                </div>
                <p class="label-descripcion">Descripcion</p>
                <p class="det-descripcion">{{instrumentoParam.descripcion}}</p>
            </div>
            <div class="det-col2-content">
                <div class="det-datos-content">
                    <p class="det-cantVentas">{{instrumentoParam.cantidad_vendida}} vendidos</p>
                    <h4 class="det-titulo">{{instrumentoParam.instrumento}}</h4>
                    <p class="det-precio">$ {{instrumentoParam.precio}}</p>
                    <p class="det-marca">Marca: {{instrumentoParam.marca}}</p>
                    <p class="det-modelo">Modelo: {{instrumentoParam.modelo}}</p>
                    <p class="det-costo">Costo de envio: 
                        <button v-if="instrumentoParam.costo_envio === 'G'" class="btn btn-success" disabled>¡Gratis!</button>
                        <span v-else>$ {{ instrumentoParam.costo_envio }}</span>
                    </p>
                    <router-link to="/" type="button" class="det-buttom-carrito">Atras</router-link>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { Instrumento } from '@/entidades/InstrumentoEntidad';

export default defineComponent({
  name: 'CardInstrumento',
  props: {
    instrumentoParam: {
      type: Instrumento,
      required: true
    }
  },
  methods: {
    getImageSource(imagen: string): string {
      return this.isExternalUrl(imagen) ? imagen : `/img/${imagen}`;
    },
    isExternalUrl(url: string): boolean | string{
      return url && url.startsWith('http');
    }
  }
});
</script>

<style>
.Detalle {
    padding: 20px;
    width: 100%;
    height: 100vh;
    background-image: linear-gradient(to right, #42b983 -20%, #2c3e50 50%, #42b983 120%);
}

.det-content {
    background-color: #FFF;
    display: grid;
    grid-template-columns: 65% 35%;
    box-shadow: 0 0 20px var(--color-principal);
    border-radius: 20px;
}

.det-col1-content {
    border-right: 2px solid #bbb;
    padding: 10px;
    grid-column: 1/ span 1;
    box-shadow: 15px 0 20px -10px rgba(0, 0, 0, 0.5);
}

.imagen-content {
    display: grid;
    align-content: center;
    justify-content: center;
}

.imagen-det {
    width: 400px;
    height: 400px;
    
}

.det-col2-content {
    padding: 15px;
    grid-column: 2 / span 1;
}

.det-cantVentas {
    margin: 0;
    font-size: 15px;
    margin-bottom: 5px;
}

.det-precio {
    font-size: 50px;
}

.det-marca {
    font-weight: 500;
    padding: 0;
    margin: 0;
}

.det-modelo{
    font-weight: 500;
    padding: 0;
    margin: 0;
}

.det-costo {
    margin: 0;
    margin-top: 20px;
}

.det-buttom-carrito {
    margin-left: 150px;
    width: 150px;
    padding: 10px 15px;
    color: rgb(61, 61, 61);
    border: 2px solid rgb(61, 61, 61);
    border-radius: 10px;
    display: grid;
    margin-top: 130px;
}

.det-buttom-carrito:hover {
    color: #fff;
    background-color: rgb(61, 61, 61);
}

.label-descripcion {
    font-weight: 700;
}
</style>
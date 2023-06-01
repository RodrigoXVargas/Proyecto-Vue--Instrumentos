<template>
    <div class="CardProducto">
          <div class="Card-Content">
              <div class="card-imagen-content">
                <img :src="getImageSource(instrumentoParam.imagen)" class="card-imagen" alt="imagen" />
              </div>
              <div class="card-datos">
                    <div class="card-datos-content">
                        <p class="card-titulo">{{instrumentoParam.instrumento}}</p>
                        <h3 class="card-precio">$ {{instrumentoParam.precio}}</h3>
                        <div class="div-btn">
                            <router-link :to="`/detalle/${instrumentoParam.id}`"><button class="btn btn-primary">Ver Detalles</button></router-link>
                        </div>
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
    isExternalUrl(url: string): boolean {
      return url.startsWith('http');
    }
  }
});
</script>
<style>
.CardProducto {
    border: 4px solid rgba(0, 0, 0, 0.2);
    border-radius: 20px;
    width: 650px;
    height: 300px;
    background-color: #FFF;
}

.CardProducto:hover {
    box-shadow: 0 0 15px var(--color-principal);
}

.CardProducto .Card-Content {
    display: grid;
    grid-template-columns: 50% 50%;
}

.card-imagen-content {
    display: grid;
    align-content: center;
    justify-content: center;
    margin: 5px;
    width: 90%;
    height: 280px;
}

.card-imagen {
    width: 280px;
    height: 280px;
}

.buttom-imagen {
    cursor: pointer;
    border: 2px solid rgba(0, 0, 0, 0.1);
    width: 100%;
    height: 100%;
}

.card-datos {
    grid-column: 2 / span 1;
    padding: 5px;
}

.card-titulo {
    font-size: 20px;
}

.card-envioGratis {
    color: rgb(0, 209, 0);
    padding-top: 10px;
}

.imagen-camion {
    width: 40px;
    height: 30px;
}

.card-envioCosto {
    color: var(--color-segundario);
}

.div-btn {
    margin-top: 60px;
}

  
</style>

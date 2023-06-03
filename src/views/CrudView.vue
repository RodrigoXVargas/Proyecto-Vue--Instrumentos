<template>
    <div class="CRUD">
        <div class='cuerpo'>
            <div class='nav_table'>
                <router-link :to="`/crud/0`"><button class='btn btn-primary' id="btn-agregar">Agregar
                        Instrumento</button></router-link>
                <input type="text" class='input-buscar' v-model="busqueda" placeholder='Buscar' />
            </div>
            <div class='table-responsive'>
                <table class="table table-dark table-hover table-sm align-middle">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>Marca</th>
                            <th>Modelo</th>
                            <th>Precio</th>
                            <th>Costo de Envio</th>
                            <th>Cantidad Vendida</th>
                            <th>Boton Modificar</th>
                            <th>Boton Eliminar</th>
                        </tr>
                    </thead>
                    <tbody class="" v-for="instrumento in instrumentosFiltrados" :key="instrumento.id">
                        <tr key={{instrumento.id}} class="RowInstrumento">
                            <th>{{ instrumento.id }}</th>
                            <td>{{ instrumento.instrumento }}</td>
                            <td>{{ instrumento.marca }}</td>
                            <td>{{ instrumento.modelo }}</td>
                            <td>{{ instrumento.precio }}</td>
                            <td>{{ instrumento.costo_envio }}</td>
                            <td>{{ instrumento.cantidad_vendida }}</td>
                            <td><router-link :to="`/crud/${instrumento.id}`"><button
                                        class="btn btn-warning">Modificar</button></router-link></td>
                            <td><button @click="deleteInstrumentoById(instrumento.id)" class="btn btn-danger">Eliminar</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>
  
<script lang="ts">
import { Instrumento } from '@/entidades/InstrumentoEntidad';
import router from '@/router';
import { defineComponent } from 'vue';


export default defineComponent({
    name: 'CrudView',
    components: {
    },
    mounted() {
        this.getAllInstrumentos();
    },
    data() {
        return {
            busqueda: '',
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
        },
        async deleteInstrumentoById(id: number) {
            let urlServer = "http://localhost:8080/api/instrumentos/delete/" + id;
            await fetch(urlServer, {
                method: 'DELETE',
                headers: {
                    'Content-type': "application/json",
                    'Access-Control-Allow-Origin': '*'
                },
                mode: 'cors'
            });
            window.location.reload();
        }
    },
    computed: {
        instrumentosFiltrados(): Instrumento[] {
            if (!this.busqueda) {
                return this.instrumentosData;
            }
            return this.instrumentosData.filter((instrumento: Instrumento) => {
                return (
                    instrumento.instrumento.toLowerCase().includes(this.busqueda.toLowerCase()) ||
                    instrumento.marca.toLowerCase().includes(this.busqueda.toLowerCase()) ||
                    instrumento.modelo.toLowerCase().includes(this.busqueda.toLocaleLowerCase())
                );
            })
        }
    }
});
</script>

<style>
.CRUD {
    background-image: linear-gradient(to right, #42b983 -20%, #2c3e50 50%, #42b983 120%);
}

.cuerpo {
    height: 100vh;
    padding: 10px;

}

table {
    text-align: center;
}

button {
    margin: 5px;
    transition-property: all;
    transition-duration: 0.2s;

}

button:hover {
    padding: 10px 20px;
    transition-property: all;
    transition-duration: 0.2s;
}

#btn-agregar {
    margin: 0;
    text-align: center;
    width: 180px;
    height: 40px;
}

#btn-agregar:hover {
    padding: 0;
    width: 200px;
    height: 45px;
}

.nav_table {
    height: 50px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}

.input-buscar {
    height: 35px;
    border-radius: 8px;
    text-align: center;
}
</style>
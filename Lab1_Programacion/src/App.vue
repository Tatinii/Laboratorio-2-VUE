<script setup>
import { ref, computed } from 'vue';

const tituloApp = ref("Planificador de Setup - UGB");
const presupuestoBase = ref(0);
const nombreArticulo = ref("");
const precioArticulo = ref(null);
const inventarioSetup = ref([]);
const errorValidacion = ref(false);

const registrarComponente = () => {
  if (nombreArticulo.value.trim() === "" || precioArticulo.value <= 0 || precioArticulo.value === null) {
    errorValidacion.value = true;
    return;
  }
  
  errorValidacion.value = false;
  inventarioSetup.value.push({
    nombre: nombreArticulo.value,
    precio: precioArticulo.value
  });
  
  nombreArticulo.value = "";
  precioArticulo.value = null;
};

const totalInvertido = computed(() => {
  return inventarioSetup.value.reduce((acumulador, item) => acumulador + item.precio, 0);
});

const saldoRestante = computed(() => presupuestoBase.value - totalInvertido.value);
</script>

<template>
  <div class="contenedor-principal">
    <h2>{{ tituloApp }}</h2>
    
    <div class="panel-presupuesto">
      <label>Presupuesto Total ($):</label>
      <input type="number" v-model.number="presupuestoBase" class="input-estandar">
      <p v-bind:class="saldoRestante < 0 ? 'alerta-peligro' : 'alerta-exito'">
        Saldo Disponible: ${{ saldoRestante }}
      </p>
    </div>

    <div class="panel-formulario">
      <input type="text" v-model="nombreArticulo" placeholder="Ej: Teclado Mecánico" class="input-estandar">
      <input type="number" v-model.number="precioArticulo" placeholder="Precio ($)" class="input-estandar">
      
      <p v-if="errorValidacion" class="mensaje-error">
        ⚠️ Error: El nombre no puede estar vacío y el precio debe ser mayor a 0.
      </p>
      
      <button @click="registrarComponente" class="boton-accion">Añadir al Presupuesto</button>
    </div>

    <div class="panel-lista">
      <h3>Componentes Proyectados</h3>
      <p v-if="inventarioSetup.length === 0" class="texto-vacio">Aún no hay componentes en tu lista.</p>
      <ul class="lista-hardware">
        <li v-for="(item, index) in inventarioSetup" :key="index">
          <span>{{ item.nombre }}</span>
          <strong>${{ item.precio }}</strong>
        </li>
      </ul>
      <hr>
      <p class="resumen-total"><strong>Inversión Total:</strong> ${{ totalInvertido }}</p>
    </div>
  </div>
</template>

<style scoped>
.contenedor-principal { max-width: 450px; margin: 2rem auto; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #ffffff; padding: 25px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
h2 { color: #004a99; text-align: center; margin-bottom: 1.5rem; }
.panel-presupuesto, .panel-formulario, .panel-lista { margin-bottom: 20px; }
label { font-weight: 600; color: #333; display: block; margin-bottom: 5px; }
.input-estandar { width: 100%; padding: 10px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box; font-size: 1rem; }
.alerta-peligro { color: #dc3545; font-weight: bold; margin-top: 5px; }
.alerta-exito { color: #28a745; font-weight: bold; margin-top: 5px; }
.mensaje-error { color: #dc3545; font-size: 0.85rem; font-weight: 600; margin-bottom: 10px; }
.boton-accion { width: 100%; background-color: #004a99; color: white; padding: 12px; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; transition: background 0.3s; }
.boton-accion:hover { background-color: #003366; }
.lista-hardware { list-style: none; padding: 0; margin: 0; }
.lista-hardware li { background: #f8f9fa; padding: 12px; margin-bottom: 8px; border-left: 4px solid #004a99; display: flex; justify-content: space-between; border-radius: 4px; }
.texto-vacio { color: #6c757d; font-style: italic; text-align: center; }
.resumen-total { text-align: right; font-size: 1.1rem; color: #333; }
</style>
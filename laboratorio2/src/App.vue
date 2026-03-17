<script setup>
import { ref, computed } from 'vue';

// Variables reactivas obligatorias 
const titulo = ref("Calculador de Setup UGB");
const presupuestoMaximo = ref(600);
const nombreArticulo = ref("");
const precioArticulo = ref(null);
const listaInversion = ref([]);
const errorActivo = ref(false);

// Función con eventos para procesar datos [cite: 9, 10]
const agregarArticulo = () => {
  if (nombreArticulo.value.trim() === "" || precioArticulo.value <= 0) {
    errorActivo.value = true;
    return;
  }
  
  errorActivo.value = false;
  listaInversion.value.push({
    nombre: nombreArticulo.value,
    precio: precioArticulo.value
  });
  
  // Limpieza de inputs 
  nombreArticulo.value = "";
  precioArticulo.value = null;
};

// Lógica adicional para el cálculo de saldo
const gastoTotal = computed(() => {
  return listaInversion.value.reduce((acc, item) => acc + item.precio, 0);
});

const saldoDisponible = computed(() => presupuestoMaximo.value - gastoTotal.value);
</script>

<template>
  <div class="setup-app">
    <h1>{{ titulo }}</h1>
    
    <div class="card">
      <label>Presupuesto Base ($):</label>
      <input type="number" v-model.number="presupuestoMaximo">
      
      <p :class="{ 'alerta': saldoDisponible < 0 }"> Saldo Restante: ${{ saldoDisponible }}
      </p>
    </div>

    <div class="formulario">
      <input type="text" v-model="nombreArticulo" placeholder="Componente (ej. Monitor)"> <input type="number" v-model.number="precioArticulo" placeholder="Precio ($)">
      
      <p v-if="errorActivo" class="error-msg">⚠️ Datos obligatorios no válidos.</p> <button @click="agregarArticulo">Añadir al Setup</button> </div>

    <ul class="lista">
      <li v-for="(item, index) in listaInversion" :key="index">
        <span>{{ item.nombre }}</span>
        <strong>${{ item.precio }}</strong>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.setup-app { max-width: 400px; margin: auto; font-family: sans-serif; padding: 20px; }
.card { background: #f0f4f8; padding: 15px; border-radius: 8px; margin-bottom: 20px; }
input { width: 100%; padding: 10px; margin: 5px 0; box-sizing: border-box; }
button { width: 100%; padding: 10px; background: #004a99; color: white; border: none; cursor: pointer; border-radius: 5px; }
.error-msg { color: #d9534f; font-size: 0.8rem; }
.alerta { color: #d9534f; font-weight: bold; }
.lista { list-style: none; padding: 0; }
li { display: flex; justify-content: space-between; padding: 10px; border-bottom: 1px solid #eee; }
</style>
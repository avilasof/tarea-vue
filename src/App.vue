<script setup>
  import { productos } from "./datos.js";
  import { ref, computed } from 'vue'

  const contador = ref(0)
  const total = productos.length
  const ruta = "https://html6.es/img/rey_"

  const siguiente = () => {
    contador.value++
    if(contador.value >= total){
      contador.value = 0
    }
  }

  const rey = computed(() => {
    const elNombre = productos[contador.value].nombre.toLowerCase()
    return elNombre.substring(0,1).toUpperCase() + elNombre.substring(1)
  })

  const imagen = computed(() => {
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
  })

  const nuevoPrecio = computed(() => {
    return Number(productos[contador.value].precio/1.10).toFixed(2)
  })

</script>

<template>
  <div class="main-div">
    <h2>Cena {{ contador + 1 }} con el rey godo: {{ rey }}</h2>
    <h3 class="precio">Precio: {{ productos[contador].precio }}</h3>
    <div v-if="productos[contador].finDeSemana" class="dias soloFinesDeSemana">(Sólo fines de semana)</div>
    <div v-else class="dias todosLosDias">(De Lunes a Domingos)</div>
    <div v-if="productos[contador].precio < 100" class="oferta">
      <div>
        Ahora un 10% dto:
        {{ nuevoPrecio }}€
        <img src="" alt="">
      </div>
    </div>
    <div class="rey">
      <img :src="imagen" alt="">
    </div>
    <button @:click="siguiente">siguiente ({{ contador + 1 }} / {{ total }})</button>
  </div>
</template>

<style lang="css" scoped>

  .main-div {
    margin: 20px;
    padding: 8px;
    border: 4px solid;
    align-items: center;
    display: inline-block;
    border-radius: 8px;
    text-align: center;
  }

  .precio {
    text-align: center
  }

  .todosLosDias {
    background-color: green;
  }

  .soloFinesDeSemana {
    background-color: red;
  }

  .dias {
    color: white;
    padding: 4px 17px;
    font-size: 0.9em;
    border-radius: 4px;
    margin: 5px 0 10px;
    display: inline-block;
  }

  .oferta {
    margin: 10px;
    padding: 5px;
  }

  .rey {
    margin: 4px;
  }

  button {
    margin-bottom: 4px;
  }
</style>

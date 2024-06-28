<script setup>
import { computed, ref } from "vue";
import { productos } from "./datos";

const numero = ref(0);
const incremento = () => {
  console.log(numero.value);
  numero.value++;
  if (numero.value >= productos.length) {
    numero.value = 0;
  }
};

const disponibilidad = computed(() => {
  return productos[numero.value].finDeSemana;
});

const descuentos = computed(() => {
  return productos[numero.value].precio < 100;
});
</script>

<template>
  <div class="flex justify-center items-center w-full h-full">
    <div
      class="border-solid border-2 border-blue-600 rounded w-1/2 flex flex-col item-center justify-center p-5"
    >
      <div class="flex justify-center items-center flex-col font-serif my-4">
        <h1 class="text-4xl">
          Cena {{ numero + 1 }} con el rey dogo
          <span class="text-green-500">{{ productos[numero].nombre }} </span>
        </h1>

        <p class="text-3xl">
          Precio:
          <span class="text-green-500">{{ productos[numero].precio }}$</span>
        </p>

        <p v-if="disponibilidad" class="bg-green-500 border-solid rounded p-3">
          <span class="text-white">(De lunes a viernes)</span>
        </p>
        <p v-else class="bg-red-500 border-solid rounded p-3">
          <span class="text-white">(Solo fines de semana)</span>
        </p>

        <p class="text-3xl flex" v-if="descuentos">
          <span class="text-red-500"
            >PRECIO CON DESCUENTO:{{ productos[numero].precio * 0.9 }}$</span
          >
          <img src="../public/oferta.jpg" alt="" class="w-20" />
        </p>
      </div>
      <div class="flex justify-center items-center flex-col my-4">
        <img
          class="w-6/12"
          :src="`https://www.html6.es/img/rey_${productos[numero].nombre}.png`"
          alt="nombre del rey"
        />
        <button
          @click="incremento"
          class="bg-red-500 border-solid border-3 border-red-200 rounded p-3 my-3"
        >
          Siguiente{{ numero + 1 }}/{{ productos.length }}
        </button>
      </div>
    </div>
  </div>
</template>

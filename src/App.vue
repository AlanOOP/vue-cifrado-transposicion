<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <main class="container mx-auto mt-5 md:mt-10 p-5 md:flex md:justify-center">
      <div class="md:w-2/3 lg:w-2/5">
        <h1 class="font-bold text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400 text-5xl capitalize text-center">
          Cifrado <span class="text-black">Transposición</span>
        </h1>

        <!-- <Alerta v-if="alerta.msg" :alerta="alerta" /> -->

        <form
          class="my-10 bg-white shadow rounded-lg p-10"
          @submit.prevent="handleSubmit"
        >
          <div class="my-5">
            <label
              for="opcion"
              class="uppercase text-gray-600 block text-xl font-bold"
            >
              Eliga una opcion:
            </label>
            <select
              class="w-full mt-3 p-3 border rounded-xl bg-gray-50"
              id="opcion"
              v-model="opcion"
            >
              <option value="">--Seleccione--</option>
              <option value="1" class="mt-3 p-3 border rounded-xl bg-gray-50">
                Cifrar
              </option>
              <option value="2" class="mt-3 p-3 border rounded-xl bg-gray-50">
                Descifrar
              </option>
            </select>
          </div>
          <div class="my-5">
            <label
              class="uppercase text-gray-600 block text-xl font-bold"
              for="text"
            >
              Ingrese su mensaje:
            </label>
            <textarea
              id="text"
              type="textarea"
              placeholder="Mensaje "
              class="w-full mt-3 p-3 border rounded-xl bg-gray-50"
              v-model="mensaje"
            />
          </div>

          <input
            type="submit"
            value="Aceptar"
            class="bg-sky-700 mb-5 w-full py-3 text-white uppercase font-bold rounded hover:cursor-pointer hover:bg-sky-800 transition-colors"
          />
        </form>

        <div class="my-2 flex">
          <label for="" class="text-3xl font-bold dark:text-white">
            Resultado:
          </label>
          <p class="text-2xl font-bold dark:text-white mt-1 ml-2 text-blue-600">{{ mensajeCifrado }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
//import Alerta from "./components/Alerta";

import C from "js-ktc";
let c = new C('secret key 123');


export default {
  // components: {
  //   Alerta,
  // },
  data() {
    return {
      count: 0,
      opcion: "",
      mensaje: "",
      mensajeCifrado: "",
      alerta: {},
    };
  },
  methods: {
    handleSubmit() {
      // console.log(this.opcion);
      // console.log(this.mensaje);

      if (this.opcion === "1") {
        const text = c.encrypt(this.mensaje);
        this.mensajeCifrado = text;
      } else if (this.opcion === "2") {
        try {
          
          const decryptedString = c.decrypt(this.mensaje);
          this.mensajeCifrado = decryptedString;
        } catch (e) {
          console.log(e);
          this.alerta = {
            msg: "El mensaje no se puede descifrar",
            error: true,
          };
          setTimeout(() => {
            this.alerta = {};
          }, 3000);
        }
      }
    },
  },
};
</script>

<style scoped>

</style>
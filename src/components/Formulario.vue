<script setup>
import { ref, reactive } from "vue";

const nombre = ref("");
const propietario = ref("");

const paciente = reactive({
    email: "",
    alta: "",
    sintomas: "",
});

const validar = () => {
    // Esto seria lo que usamos generalmente pero en Vue se puede acortar este paso
    // e.preventDefault(); Eliminarmos esta linea, la dejamos como una arrowFuncion normal y usamos lo que se llama modificadores de eventos @submit.prevent
    console.log("Validando");
    if ([nombre.value, propietario.value].includes("")) {
        return console.log("Campo nombre y propietario son obligatorios");
    }
    if (Object.values(paciente).includes("")) {
        return console.log("Todos los campos son obligatorios");
    }
};
</script>
<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">
            Seguimiento de Pacientes
        </h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600">Administralos</span>
        </p>
        <form
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            @submit.prevent="validar"
        >
            <div class="mb-5">
                <label
                    for="mascota"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Mascota
                </label>
                <input
                    id="mascota"
                    type="text"
                    placeholder="Nombre de la Mascota"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="nombre"
                    v-on:input="(e) => (nombre = e.target.value)"
                />
            </div>
            <div class="mb-5">
                <label
                    for="propietario"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Propietario
                </label>
                <input
                    id="propietario"
                    type="text"
                    placeholder="Nombre del Propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-model="propietario"
                />
                <!-- v-model es lo mismo que :value="nombre"
                    v-on:input="(e) => (nombre = e.target.value)"-->
            </div>
            <div class="mb-5">
                <label
                    for="email"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Email
                </label>
                <input
                    id="email"
                    type="email"
                    placeholder="Email del Propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-model="paciente.email"
                />
            </div>
            <div class="mb-5">
                <label
                    for="alta"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Alta
                </label>
                <input
                    id="alta"
                    type="date"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-model="paciente.alta"
                />
            </div>
            <div class="mb-5">
                <label
                    for="sintomas"
                    class="block text-gray-700 uppercase font-bold"
                >
                    sintomas
                </label>
                <textarea
                    id="sintomas"
                    placeholder="Describe los Sintomas"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-model="paciente.sintomas"
                >
                </textarea>
            </div>
            <input
                type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar Paciente"
            />
        </form>
    </div>
</template>
import { fromJSON } from 'postcss';

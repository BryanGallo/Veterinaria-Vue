<script setup>
import { ref, reactive } from "vue";
import Alerta from "./Alerta.vue";

const alerta = reactive({
    mensaje: "",
    tipo: "",
});

const props = defineProps({
    nombre: {
        type: String,
        required: true,
    },
    propietario: {
        type: String,
        required: true,
    },
    email: {
        type: String,
        required: true,
    },
    alta: {
        type: String,
        required: true,
    },
    sintomas: {
        type: String,
        required: true,
    },
});

const emit = defineEmits([
    "update:nombre",
    "update:propietario",
    "update:email",
    "update:alta",
    "update:sintomas",
    "guardar-paciente",
]);

const validar = () => {
    // Esto seria lo que usamos generalmente pero en Vue se puede acortar este paso
    // e.preventDefault(); Eliminarmos esta linea, la dejamos como una arrowFuncion normal y usamos lo que se llama modificadores de eventos @submit.prevent
    console.log("Validando");
    if (Object.values(props).includes("")) {
        console.log("Todos los campos son obligatorios");
        alerta.mensaje = "Todos los campos son obligatorios";
        alerta.tipo = "error";
        return;
    }

    emit("guardar-paciente");
    alerta.mensaje = "Paciente Almacenado Correctamente";
    alerta.tipo = "exito";

    setTimeout(() => {
        Object.assign(alerta, {
            mensaje: "",
            tipo: "",
        });
    }, 3000);
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
        <Alerta v-if="alerta.mensaje" :alerta="alerta" />
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
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md uppercase"
                    :value="nombre"
                    @input="
                        $emit(
                            'update:nombre',
                            $event.target.value.toUpperCase()
                        )
                    "
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
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md uppercase"
                    :value="propietario"
                    @input="
                        $emit(
                            'update:propietario',
                            $event.target.value.toUpperCase()
                        )
                    "
                />
                <!-- v-model="propietario" es lo mismo que 
                    :value="nombre"
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
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md lowercase"
                    :value="email"
                    @input="
                        $emit('update:email', $event.target.value.toLowerCase())
                    "
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
                    :value="alta"
                    @input="$emit('update:alta', $event.target.value)"
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
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md uppercase"
                    :value="sintomas"
                    @input="
                        $emit(
                            'update:sintomas',
                            $event.target.value.toUpperCase()
                        )
                    "
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

<script setup>
import Paciente from "./Paciente.vue";

defineEmits(["actualizar-paciente", "eliminarPaciente"]);
const props = defineProps({
    pacientes: {
        type: Array,
        required: true,
    },
});
</script>
<template>
    <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h2 className="font-black text-3xl text-center">
            Listado de Pacientes
        </h2>
        <p className="text-lg my-5 text-center">
            Administra tus
            <span className="text-indigo-600 font-bold">
                Pacientes y Citas
            </span>
        </p>
        <div v-if="pacientes.length > 0" class="text-center">
            <Paciente
                v-for="paciente in pacientes"
                :paciente="paciente"
                @actualizar-paciente="(id) => $emit('actualizar-paciente', id)"
                @eliminar-paciente="(id) => $emit('eliminar-paciente', id)"
            />
        </div>
        <p v-else class="text-center text-2xl mt-10">
            No existen pacientes agregalos
        </p>
    </div>
</template>

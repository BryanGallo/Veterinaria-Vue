<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";
import ListadoPacientes from "./components/ListadoPacientes.vue";
const pacientes = ref([]);

const paciente = reactive({
    nombre: "",
    propietario: "",
    email: "",
    alta: "",
    sintomas: "",
});

const guardarPaciente = () => {
    pacientes.value.push(paciente);

};
</script>

<template>
    <div class="container mx-auto mt-20">
        <Header />
        <div class="mt-12 md:flex">
            <Formulario
                v-model:nombre="paciente.nombre"
                v-model:propietario="paciente.propietario"
                v-model:email="paciente.email"
                v-model:alta="paciente.alta"
                v-model:sintomas="paciente.sintomas"
                @guardar-paciente="guardarPaciente"
            />
            <ListadoPacientes :pacientes="pacientes" />
        </div>
    </div>
</template>

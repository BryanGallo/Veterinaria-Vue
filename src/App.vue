<script setup>
import { ref, reactive } from "vue";
import { uid } from "uid";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import ListadoPacientes from "./components/ListadoPacientes.vue";
const pacientes = ref([]);

const paciente = reactive({
    id: null,
    nombre: "",
    propietario: "",
    email: "",
    alta: "",
    sintomas: "",
});

const guardarPaciente = () => {
    if (paciente.id) {
        console.log(paciente.id);
        const i = pacientes.value.findIndex((pacienteState) => {
            return pacienteState.id === paciente.id;
        });
        console.log(pacientes.value[i]);
        console.log({ ...paciente });
        pacientes.value[i] = { ...paciente };
    } else {
        pacientes.value.push({ ...paciente, id: uid() });
        //Objetc.asssign sirve para  recorrer un objeto y cambiar sus valores es como usar paciente.nombre =""
    }
    Object.assign(paciente, {
        nombre: "",
        propietario: "",
        email: "",
        alta: "",
        sintomas: "",
        id: null,
    });
};

const actualizarPaciente = (id) => {
    console.log(id);
    const pacienteEditar = pacientes.value.filter(
        (paciente) => paciente.id === id
    )[0];
    console.log(pacienteEditar);
    Object.assign(paciente, pacienteEditar);
};

const eliminarPaciente = (id) => {
    pacientes.value = pacientes.value.filter((paciente) => id !== paciente.id);

};
</script>

<template>
    <div class="container mx-auto mt-20">
        <Header />
        <div class="mt-12 md:flex">
            <Formulario
                :id="paciente.id"
                v-model:nombre="paciente.nombre"
                v-model:propietario="paciente.propietario"
                v-model:email="paciente.email"
                v-model:alta="paciente.alta"
                v-model:sintomas="paciente.sintomas"
                @guardar-paciente="guardarPaciente"
            />
            <ListadoPacientes
                :pacientes="pacientes"
                @actualizar-paciente="actualizarPaciente"
                @eliminar-paciente="eliminarPaciente"
            />
        </div>
    </div>
</template>

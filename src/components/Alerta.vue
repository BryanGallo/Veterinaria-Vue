<script setup>
import { computed } from "vue";
const props = defineProps({
    alerta: {
        type: Object,
        require: true,
    },
});
//Se una un computed property debido a que es reactivo y es una forma de mantener el template limpio
const isError = computed(()=>{
    return props.alerta.tipo === 'error'
});
</script>
<template>
    <!-- para usar un ternario usamos [] -->
    <div
        :class="[isError ? 'bg-red-500':'bg-green-500']"
        class="text-white text-center p-3 uppercase font-bold rounded-md mb-3"
    >
        {{ alerta.mensaje }}
    </div>
</template>

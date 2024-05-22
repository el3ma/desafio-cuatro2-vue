<template>
    <div class="cardPaciente col mx-2">
        <div class=" text-center p-5 card-body">
            <h4>Paciente</h4>
            <p>{{ nombre }}</p>
            <h4>Fecha</h4>
            <p>{{ fecha }}</p>
            <h4>Hora</h4>
            <p>{{ hora }}</p>
            <h4>Motivo</h4>
            <p>{{ motivo }}</p>
            <button class="btn btn-danger" @click="$emit('eliminarPaciente')">Eliminar</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardPaciente',
    props:{
        nombre: String,
        fecha: String,
        hora: String,
        motivo: String
    }
}
</script>

<style scoped>

</style>
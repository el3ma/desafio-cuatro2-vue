<template>
  <div id="app" class="container">
    <section class="border border-2 border-secondary rounded m-5">
      <form class="col my-5" @submit.prevent="agregarPaciente">
        <div class="d-flex justify-content-around">
          <div class="col-2 mx-3">
            <label for="paciente" class="form-label" :class="{ noActivo: !datosPaciente.nombre }">Paciente</label>
            <input type="text" id="paciente" class="form-control" v-model="datosPaciente.nombre">
          </div>
          <div class="col-2 mx-3">
            <label for="fecha" class="form-label" :class="{ noActivo: !datosPaciente.fecha }">Fecha</label>
            <input type="date" id="fecha" class="form-control" v-model="datosPaciente.fecha">
          </div>
          <div class="col-2 mx-3">
            <label for="hora" class="form-label" :class="{ noActivo: !datosPaciente.hora }">Hora</label>
            <input type="time" id="hora" class="form-control" v-model="datosPaciente.hora">
          </div>
          <div class="col-2 mx-3">
            <label for="gravedad" class="form-label" :class="{ noActivo: !datosPaciente.gravedad }">Gravedad</label>
            <select class="form-select" id="gravedad" v-model="datosPaciente.gravedad">
              <option v-for="(gravedad, index) in tiposGravedad" :key="index">{{ gravedad }}</option>
            </select>
          </div>
          <div class="col-2 mx-3">
            <label for="motivo" class="form-label" :class="{ noActivo: !datosPaciente.motivo }">Motivo</label>
            <input type="text" id="motivo" class="form-control" v-model="datosPaciente.motivo">
          </div>
        </div>
        <div class="text-center py-3">
          <button class="btn btn-secondary px-5" :disabled="!botonActivo">Agregar</button>
        </div>
      </form>
    </section>
    <section class="">
      <div class="row row-cols-lg-6 g-2 justify-content-evenly">

        <CardPaciente v-for="(paciente, index) in listaPacientes" :key="index" :style="colorFondo(paciente.gravedad)"
          :nombre="paciente.nombre" :fecha="paciente.fecha" :hora="paciente.hora" :motivo="paciente.motivo"
          @eliminarPaciente="listaPacientes.splice(index, 1)" />


      </div>

    </section>
  </div>
</template>

<script>
import CardPaciente from "./components/CardPaciente.vue"

export default {
  name: 'App',
  components: {
    CardPaciente
  },
  data() {
    return {
      tiposGravedad: ['Baja', 'Media', 'Alta'],
      datosPaciente: { nombre: '', fecha: '', hora: '', gravedad: '', motivo: '' },
      listaPacientes: [
        { nombre: 'pedrito', fecha: '12-12-2024', hora: '13:15', gravedad: 'Baja', motivo: 'Dolor pie' },
        { nombre: 'pedrito', fecha: '22-05-2024', hora: '12:15', gravedad: 'Media', motivo: 'dolor guatita' },
        { nombre: 'pedrito', fecha: '23-05-2024', hora: '12:45', gravedad: 'Alta', motivo: 'Dolor Mano' },
        { nombre: 'pedrito', fecha: '23-05-2024', hora: '12:45', gravedad: 'Alta', motivo: 'Dolor Mano' },
        { nombre: 'pedrito', fecha: '23-05-2024', hora: '12:45', gravedad: 'Alta', motivo: 'Dolor Mano' },
        { nombre: 'pedrito', fecha: '23-05-2024', hora: '12:45', gravedad: 'Alta', motivo: 'Dolor Mano' },
        { nombre: 'pedrito', fecha: '23-05-2024', hora: '12:45', gravedad: 'Alta', motivo: 'Dolor Mano' },
        { nombre: 'pedrito', fecha: '23-05-2024', hora: '12:45', gravedad: 'Alta', motivo: 'Dolor Mano' }
      ]
    }
  },
  methods: {
    agregarPaciente: function () {
      const nuevoPaciente = Object.assign({}, this.datosPaciente);
      this.listaPacientes.push(nuevoPaciente);
      this.datosPaciente = { nombre: '', fecha: '', hora: '', gravedad: '', motivo: '' }
    },
    colorFondo: function (gravedad) {
      if (gravedad === 'Baja') {
        return 'background-color : #8DECB4;'
      } else if (gravedad === 'Media') {
        return 'background-color: #FFFAB7;'
      } else if (gravedad === 'Alta') {
        return 'background-color: #FF204E'
      }
    }
  },
  computed: {
    botonActivo: function () {
      return this.datosPaciente.nombre && this.datosPaciente.fecha && this.datosPaciente.hora && this.datosPaciente.gravedad && this.datosPaciente.motivo
    }
  }
}
</script>

<style>
.noActivo {
  color: red;
}
</style>

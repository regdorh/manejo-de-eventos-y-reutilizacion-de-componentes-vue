<template>
  <h1>Home</h1>
  <main class="container">
    <!-- Seccion reserva de citas -->
    <section class="mb-5">
      <form class="border rounded-3 p-4" @submit.prevent="crearCita">
        <div class="row mb-3">
          <div class="col-3">
            <label for="paciente" :class="[!citaActual.paciente ? 'text-danger' : '']">Paciente</label>
            <input type="text" class="form-control" id="paciente" v-model="citaActual.paciente">
          </div>
          <div class="col-2">
            <label for="fecha" :class="[!citaActual.fecha ? 'text-danger' : '']">Fecha</label>
            <input type="date" class="form-control" id="fecha" v-model="citaActual.fecha">
          </div>
          <div class="col-2">
            <label for="hora" :class="[!citaActual.hora ? 'text-danger' : '']">Hora</label>
            <input type="time" class="form-control" id="hora" v-model="citaActual.hora">
          </div>
          <div class="col-2">
            <label for="gravedad" :class="[!citaActual.gravedad ? 'text-danger' : '']">Gravedad</label>
            <select class="form-control" id="gravedad" v-model="citaActual.gravedad">
              <option disabled value="" selected>Selecciona una opción</option>
              <option :value="gravedad" v-for="(gravedad, index) in gravedades" :key="index">{{ gravedad }}</option>
            </select>
          </div>
          <div class="col-3">
            <label for="motivo" :class="[!citaActual.motivo ? 'text-danger' : '']">Motivo</label>
            <input type="text" class="form-control" id="motivo" v-model="citaActual.motivo">
          </div>
        </div>
        <div class="d-flex justify-content-center">
          <button type="submit" class="btn btn-primary" :class="{ disabled: buttonDisabled }">Agregar</button>
        </div>
      </form>
    </section>

    <!-- Seccion de citas -->
    <section>
      <div v-if="citas.length">
        <div class="row">
          <div class="col-12 col-md-6 col-lg-3" v-for="(cita, index) in citas" :key="index">
            <CardCitaComp :cita="cita" :index="index" @delete="deleteCita" />
          </div>
        </div>
      </div>
      <div v-else>
        <p class="text-danger text-center">Aún no hay citas registradas.</p>
      </div>
    </section>
  </main>
</template>

<script>
import CardCitaComp from '@/components/CardCitaComp.vue'

export default {
  name: 'App',
  data() {
    return {
      citaActual: {
        paciente: '',
        fecha: '',
        hora: '',
        gravedad: '',
        motivo: '',
      },
      gravedades: ['Baja', 'Media', 'Alta'],
      citas: []
    }
  },
  computed: {
    buttonDisabled() {
      return !this.citaActual.paciente || !this.citaActual.fecha || !this.citaActual.hora || !this.citaActual.gravedad || !this.citaActual.motivo;
    }
  },
  methods: {
    crearCita() {
      let newCita = { ...this.citaActual };
      this.citas.push(newCita);
      // Vaciar formulario
      this.citaActual = {
        paciente: '',
        fecha: '',
        hora: '',
        gravedad: '',
        motivo: ''
      };
    },
    deleteCita(index) {
      this.citas.splice(index, 1)
    }
  },
  components: {
    CardCitaComp
  }

}
</script>

<style></style>

<template>
    <div class="card" :class="[cita.gravedad == 'Baja' ? 'bg-success' : cita.gravedad == 'Media' ? 'bg-warning' : 'bg-danger']">
        <div class="card-body" :class="{'text-dark': cita.gravedad == 'Media'}">
            <h5 class="card-title">Paciente</h5>
            <p class="card-text">{{ cita.paciente }}</p>
            <h5 class="card-title">Fecha</h5>
            <p class="card-text">{{ cita.fecha }}</p>
            <h5 class="card-title">Hora</h5>
            <p class="card-text">{{ cita.hora }}</p>
            <h5 class="card-title">Motivo</h5>
            <p class="card-text">{{ cita.motivo }}</p>
            <button class="btn" :class="[cita.gravedad=='Media' ? 'btn-outline-dark' : 'btn-outline-light']" @click="$emit('delete',index)">Eliminar</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardCitaComp',
    props: {
        cita: Object, 
        index: Number
    },
    data: function () {
        return {}
    },
  
}
</script>

<style scoped></style>
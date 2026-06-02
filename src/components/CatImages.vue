<template>
    <div class="text-secondary p-3 text-center">
        <button @click="buscarGatito" class="btn btn-info text-white fw-semibold shadow-sm px-4 py-2 rounded-pill">Buscar una imagen de un gatito :3</button>
        <br><br>
        <div v-if="cargando" class="spinner-border text-info" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>

    <div class="d-flex justify-content-center">
        <img v-if="URLGatito" :src="URLGatito.url" alt="Un gatito!" class="img-fluid rounded-4 shadow-sm m-3" style="max-height: 450px; object-fit: cover;">
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const cargando = ref(false)
const URLGatito = ref(null)

const buscarGatito = async () => {
    cargando.value = true
    URLGatito.value = null
    const respuesta = await fetch('https://api.thecatapi.com/v1/images/search')
    const dato = await respuesta.json()
    URLGatito.value = dato[0]
    cargando.value = false
}

onMounted(() => {
    document.body.className = "bg-body-secondary font-sans-serif min-vh-100"
})
</script>
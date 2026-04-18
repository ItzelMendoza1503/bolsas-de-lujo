<script setup>
import { ref } from 'vue'

const formulario = ref({
  nombre: '',
  correo: '',
  telefono: '',
  bolso_de_interes: '' // Este nombre coincide con tu columna en Google Sheets
})

const enviando = ref(false)
const mensajeStatus = ref('')

const enviarDatos = async () => {
  enviando.value = true
  
  // Tu nueva URL actualizada
  const scriptURL = 'https://script.google.com/macros/s/AKfycbzi73EoXQ9tESA-Qxtj7Bnq5YIkYCpU1RmqmUnBCRXTF_kmQkwfkEnnAvCTpHaYuZ7b/exec'

  try {
    // Usamos URLSearchParams para emular un envío de formulario estándar (x-www-form-urlencoded)
    const params = new URLSearchParams()
    params.append('nombre', formulario.value.nombre)
    params.append('correo', formulario.value.correo)
    params.append('telefono', formulario.value.telefono)
    params.append('bolso_de_interes', formulario.value.bolso_de_interes)

    await fetch(scriptURL, {
      method: 'POST',
      mode: 'no-cors', // Crucial para evitar errores de política de CORS
      body: params
    })

    // Como usamos 'no-cors', el navegador no puede leer la respuesta de éxito, 
    // así que asumimos que llegó si no saltó al 'catch'.
    mensajeStatus.value = "¡Solicitud recibida! Los datos se han guardado en nuestra base de datos."
    formulario.value = { nombre: '', correo: '', telefono: '', bolso_de_interes: '' }
    
  } catch (error) {
    mensajeStatus.value = "Hubo un error al conectar con el servidor."
    console.error('Error:', error)
  } finally {
    enviando.value = false
  }
}
</script>

<template>
  <div style="max-width: 500px; margin: 40px auto; font-family: 'Helvetica Neue', Arial, sans-serif; padding: 40px; border-radius: 12px; background: #fff; box-shadow: 0 10px 30px rgba(0,0,0,0.1); border: 1px solid #e5e7eb;">
    
    <div style="text-align: center; margin-bottom: 30px;">
      <h2 style="color: #111; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 8px;">Contacto de Boutique</h2>
      <p style="color: #b08d57; font-size: 0.9rem;">Consulta de Disponibilidad y Pedidos</p>
    </div>

    <form @submit.prevent="enviarDatos" style="display: flex; flex-direction: column; gap: 15px;">
      <div>
        <label style="display: block; font-size: 0.8rem; color: #4b5563; margin-bottom: 5px;">Nombre Completo</label>
        <input v-model="formulario.nombre" placeholder="Escribe tu nombre" required style="width: 100%; padding: 12px; border: 1px solid #d1d5db; border-radius: 6px;">
      </div>

      <div>
        <label style="display: block; font-size: 0.8rem; color: #4b5563; margin-bottom: 5px;">Correo Electrónico</label>
        <input v-model="formulario.correo" type="email" placeholder="email@ejemplo.com" required style="width: 100%; padding: 12px; border: 1px solid #d1d5db; border-radius: 6px;">
      </div>

      <div>
        <label style="display: block; font-size: 0.8rem; color: #4b5563; margin-bottom: 5px;">Teléfono</label>
        <input v-model="formulario.telefono" type="tel" placeholder="Número de contacto" required style="width: 100%; padding: 12px; border: 1px solid #d1d5db; border-radius: 6px;">
      </div>

      <div>
        <label style="display: block; font-size: 0.8rem; color: #4b5563; margin-bottom: 5px;">Modelo de Bolso de Interés</label>
        <textarea v-model="formulario.bolso_de_interes" placeholder="¿Qué modelo deseas consultar?" required style="width: 100%; padding: 12px; border: 1px solid #d1d5db; border-radius: 6px; height: 100px; resize: none;"></textarea>
      </div>
      
      <button type="submit" :disabled="enviando" style="background: #1a1a1a; color: white; border: none; padding: 15px; cursor: pointer; font-weight: bold; border-radius: 6px; margin-top: 10px;">
        {{ enviando ? 'PROCESANDO...' : 'ENVIAR SOLICITUD' }}
      </button>
    </form>
    
    <p v-if="mensajeStatus" style="text-align: center; margin-top: 20px; font-weight: bold; color: #155724; background: #d4edda; padding: 12px; border-radius: 6px; border: 1px solid #c3e6cb;">
      {{ mensajeStatus }}
    </p>
    
    <NuxtLink to="/" style="display: block; text-align: center; margin-top: 25px; color: #6b7280; text-decoration: none; font-size: 0.85rem;">← Volver al Catálogo</NuxtLink>
  </div>
</template>
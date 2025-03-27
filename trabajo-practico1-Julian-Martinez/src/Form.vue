<template>
  <div id="app">
    <div class="box-container">
      <h1>Formulario de Usuario</h1>
      <form @submit.prevent="submitForm">
        <div class="input-group">
          <label for="username">Nombre de Usuario:</label>
          <input v-model="usuario.nombre" type="text" id="username" required />
        </div>
        <div class="input-group">
          <label for="email">Email:</label>
          <input v-model="usuario.email" type="email" id="email" required />
        </div>
        <div class="input-group">
          <label for="password">Contraseña:</label>
          <input v-model="usuario.password" type="password" id="password" required />
        </div>
        <div class="input-group">
          <label for="birthdate">Fecha de Nacimiento:</label>
          <input v-model="usuario.fechaNacimiento" type="date" id="birthdate" required />
        </div>
        <button type="submit">Crear Usuario</button>
      </form>
      
      <div v-if="usuario.creado" class="user-info">
        <h2>Datos del Usuario</h2>
        <p><strong>Nombre:</strong> {{ usuario.nombre }}</p>
        <p><strong>Email:</strong> {{ usuario.email }}</p>
        <p><strong>Edad:</strong> {{ usuario.edad }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const usuario = ref({
  nombre: '',
  email: '',
  password: '',
  fechaNacimiento: '',
  creado: false,
  edad: 0,
});

const calcularEdad = (fechaNacimiento) => {
  const today = new Date();
  const birthDate = new Date(fechaNacimiento);
  let age = today.getFullYear() - birthDate.getFullYear();
  const m = today.getMonth() - birthDate.getMonth();
  if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) {
    age--;
  }
  return age;
};

const submitForm = () => {
  usuario.value.edad = calcularEdad(usuario.value.fechaNacimiento);
  usuario.value.creado = true;
  alert(`Usuario creado con éxito: \nNombre: ${usuario.value.nombre} \nEmail: ${usuario.value.email} \nEdad: ${usuario.value.edad}`);
  
  usuario.value.nombre = '';
  usuario.value.email = '';
  usuario.value.password = '';
  usuario.value.fechaNacimiento = '';
};
</script>

<style scoped>

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #667eea, #764ba2);
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
}


.box-container {
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    padding: 30px;
    width: 350px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    text-align: center;
}


form {
    display: flex;
    flex-direction: column;
    width: 100%;
   
}


.input-group {
    margin-bottom: 20px;
    text-align: left;
}


label {
    font-size: 14px;
    font-weight: bold;
    color: white;
    display: block;
    margin-bottom: 5px;
}


input {
    width: 100%;
    padding: 10px;
    border: none;
    border-radius: 10px;
    font-size: 16px;
    background: rgba(255, 255, 255, 0.3);
    color: white;
    outline: none;
    transition: 0.3s;
}

input::placeholder {
    color: rgba(255, 255, 255, 0.7);
}

input:focus {
    background: rgba(255, 255, 255, 0.4);
}

/* Botón */
button {
    width: 100%;
    padding: 12px;
    background: rgba(255, 255, 255, 0.3);
    border: none;
    color: white;
    font-size: 16px;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: rgba(255, 255, 255, 0.5);
}

/* Estilo de la información del usuario */
.user-info {
    margin-top: 20px;
    background: rgba(255, 255, 255, 0.2);
    padding: 15px;
    border-radius: 10px;
    color: white;
    text-align: left;
}
</style>

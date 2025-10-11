<template>
  <div class="auth-page-container">
    <img
      class="background-image"
      src="https://cdn-proxymedia-digicert.tv-fr-cdn.orange.net/api/v1/images/2329%2F14794a8b553b48fdaf0cad11278c591a.jpg?service=guidetv&device=W_PC"
      alt="Fondo"
    />
    <div class="auth-box">
      <img src="/logo.svg" alt="PortalDev News Logo" class="auth-logo" />

      <h3 class="auth-title">Registrarse</h3>

      <div class="social-login">
        <p class="social-text">Con redes sociales</p>
        <button class="social-btn google-btn">
          <i class="bi bi-google"></i> Iniciar sesión con Google
        </button>
        <button class="social-btn facebook-btn">
          <i class="bi bi-facebook"></i> Iniciar sesión con Facebook
        </button>
        <button class="social-btn apple-btn">
          <i class="bi bi-apple"></i> Iniciar sesión con Apple
        </button>
      </div>

      <div class="separator"><span>ó</span></div>

      <form @submit.prevent="handleRegister" class="auth-form">
        <div class="form-group">
          <label for="email">Email*</label>
          <input type="email" id="email" v-model="registro.email" required />
        </div>

        <div class="form-group">
          <label for="password">Contraseña*</label>
          <div class="password-input-wrapper">
            <input :type="passwordFieldType" id="password" v-model="registro.password" required />

            <button type="button" class="btn-toggle-password" @click="togglePasswordVisibility">
              <i
                :class="
                  passwordFieldType === 'password' ? 'bi bi-eye-slash-fill' : 'bi bi-eye-fill'
                "
              ></i>
            </button>
          </div>
        </div>

        <button type="submit" class="btn-primary">Registrarse</button>
      </form>

      <p class="auth-footer-link">
        ¿Ya tenés una cuenta? <router-link to="/iniciar-sesion">Iniciar sesión</router-link>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue' // 💡 Importamos 'computed'

const registro = ref({
  email: '',
  password: '',
})

// Estado para controlar si la contraseña es visible o no (inicialmente oculta)
const isPasswordVisible = ref(false)

// Propiedad computada que define el 'type' del input ('password' o 'text')
const passwordFieldType = computed(() => {
  return isPasswordVisible.value ? 'text' : 'password'
})

// Función para alternar la visibilidad
const togglePasswordVisibility = () => {
  isPasswordVisible.value = !isPasswordVisible.value
}

const handleRegister = () => {
  console.log('Intentando registrar:', registro.value)
  alert('Registrandose...')
}
</script>

<style scoped>
/* Contenedor centralizado */
.auth-page-container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.auth-page-container::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  pointer-events: none;
  z-index: 1;
}

/* Imagen de fondo a pantalla completa */
.background-image {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  pointer-events: none;
  z-index: 0;
}

.auth-box {
  background: rgba(255, 255, 255, 0.95);
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(8px);
  width: 100%;
  max-width: 400px;
  text-align: center;
  z-index: 2;
}

.auth-logo {
  /* Controla el tamaño de la imagen */
  width: 300px; /* Ajusta este valor al tamaño real de tu logo InfoExpress */
  height: auto;

  /* Asegura que la imagen esté centrada */
  display: block;
  margin-left: auto;
  margin-right: auto;

  /* Margen inferior para separarlo del título */
  margin-bottom: 30px;
}

.auth-title {
  font-size: 1.6em;
  font-weight: 500;
  margin-bottom: 25px;
}

/* Redes Sociales */
.social-login {
  margin-bottom: 25px;
}

.social-text {
  font-size: 0.9em;
  color: #333;
  margin-bottom: 10px;
}

.social-btn {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.2s;
}

.social-btn i {
  margin-right: 10px;
  font-size: 1.2em;
}

.social-btn:hover {
  background-color: #f0f0f0;
}

/* Separador "ó" */
.separator {
  display: flex;
  align-items: center;
  text-align: center;
  color: #a1a1a1;
  margin: 20px 0;
}
.separator::before,
.separator::after {
  content: '';
  flex: 1;
  border-bottom: 1px solid #d3d3d3;
}
.separator:not(:empty)::before {
  margin-right: 0.25em;
}
.separator:not(:empty)::after {
  margin-left: 0.25em;
}

/* Formulario */
.auth-form {
  text-align: left;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  font-size: 0.9em;
  color: #333;
  margin-bottom: 5px;
}

/* NUEVO: Contenedor del campo de contraseña */
.password-input-wrapper {
  position: relative; /* CLAVE: Punto de referencia para el botón 'toggle' */
  display: flex; /* Asegura que el input y el botón se alineen (aunque el botón esté absolute) */
  align-items: center;
}

/* Ajuste del Input para dejar espacio al icono */
.form-group input {
  /* Mantenemos width: 100% */
  width: 100%;
  padding: 10px;
  /* 💡 Ajuste: Añadir padding a la derecha para que el texto no se oculte detrás del botón */
  padding-right: 40px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1em;
  box-sizing: border-box;
}

/* NUEVO: Botón de alternancia de contraseña (el ojo) */
.btn-toggle-password {
  position: absolute; /* Flota sobre el input */
  right: 1px; /* Pegado al borde derecho */
  top: 50%;
  transform: translateY(-50%); /* Centrado verticalmente */

  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  color: #777; /* Color sutil */
  line-height: 1;
  transition: color 0.2s;
}

.btn-toggle-password:hover {
  color: #333; /* Resalta al pasar el ratón */
}

.btn-toggle-password i {
  font-size: 1.5em; /* Ajusta el tamaño del icono de Bootstrap */
}

.btn-primary {
  width: 100%;
  padding: 10px;
  background-color: #007bff; /* Azul primario */
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1em;
  font-weight: bold;
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.2s;
}

.btn-primary:hover {
  background-color: #0056b3;
}

/* Pie de página del formulario */
.auth-footer-link {
  margin-top: 20px;
  font-size: 0.9em;
}

.auth-footer-link a {
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
}
</style>

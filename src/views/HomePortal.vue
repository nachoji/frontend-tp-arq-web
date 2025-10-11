<template>
  <div>
    <BarraSuperior />

    <header class="portal-header-principal">
      <div class="header-inner">
        <img src="/logo.svg" alt="PortalDev News Logo" class="logo-img" />

        <div class="header-acciones">
          <router-link to="/registro" class="btn-suscripcion">Registrate GRATIS</router-link>
          <router-link to="/iniciar-sesion" class="btn-ingreso">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-person-fill"
              viewBox="0 0 16 16"
            >
              <path
                d="M3 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H3zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"
              />
            </svg>
            Ingresar
          </router-link>
        </div>
      </div>
    </header>

    <nav class="portal-nav-menu">
      <div class="menu-inner">
        <SearchBar />
        <a href="#">ÚLTIMO MOMENTO</a>
        <a href="#">POLÍTICA</a>
        <a href="#">ECONOMÍA</a>
        <a href="#">RURAL</a>
        <a href="#">SOCIEDAD</a>
        <a href="#">MUNDO</a>
        <a href="#">DEPORTES</a>
        <a href="#">ESPECTÁCULOS</a>
      </div>
    </nav>

    <main class="portal-principal-grid">
      <section class="columna-principal-noticia">
        <div class="seccion-principal-noticia">
          <ArticuloCard
            v-for="articulo in articulosPrincipales"
            :key="articulo.id"
            :articulo="articulo"
          />
        </div>
      </section>

      <aside class="columna-lateral-feed">
        <ArticuloCard
          v-for="articulo in feedArticulos.slice(0, 2)"
          :key="articulo.id"
          :articulo="articulo"
          tipo-vista="secundaria-lateral"
        />
      </aside>
    </main>

    <section class="portal-fila-inferior">
      <ArticuloCard
        v-for="articulo in articulosFilaInferior"
        :key="articulo.id"
        :articulo="articulo"
        tipo-vista="miniatura-card"
      />
    </section>

    <footer class="portal-footer">
      <p>Todos Los Derechos Reservados &copy; 2025 InfoExpress</p>
    </footer>
  </div>
</template>

<script setup>
import { noticiasPrincipales, feedArticulos, noticiasFilaInferior } from '@/data/mockData.js'
import ArticuloCard from '@/components/ArticuloCard.vue'
import BarraSuperior from '@/components/BarraSuperior.vue'
import SearchBar from '@/components/SearchBar.vue'
import { ref } from 'vue'

const articulosPrincipales = ref(noticiasPrincipales)
const articulosFilaInferior = ref(noticiasFilaInferior)
</script>

<style scoped>
.portal-header-principal {
  padding: 20px 0;
  border-bottom: 1px solid #ddd;
}

.header-inner {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 30px;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-acciones {
  display: flex;
  align-items: center;
  gap: 10px;
}

.btn-suscripcion {
  background-color: #006dff;
  color: #fff;
  font-weight: bold;
  border: none;
  padding: 10px 20px;
  border-radius: 50px;
  cursor: pointer;
}

.btn-suscripcion:hover {
  background-color: #0056cc;
}

.btn-ingreso {
  background-color: #fff;
  color: #333;
  font-weight: bold;
  border: 1px solid #ccc;
  padding: 10px 20px;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 5px;
}

.btn-ingreso:hover {
  background-color: #f0f0f0;
}

.portal-nav-menu {
  padding: 10px 0;
  border-bottom: 1px solid #eee;
  margin-bottom: 40px;
  font-size: 0.9em;
  font-weight: bold;
}

.menu-inner {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 30px;

  display: flex;
  align-items: center;
  gap: 20px;
}

.menu-inner a {
  text-decoration: none;
  color: #333;
  text-transform: uppercase;
}

.portal-header {
  border-bottom: 1px solid #eee;
  padding: 30px 0;
  margin-bottom: 40px;
}

.logo-y-nav {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.portal-nav a {
  margin-left: 20px;
  text-decoration: none;
  color: #333;
  font-weight: bold;
}

.portal-principal-grid {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 30px;

  display: grid;
  grid-template-columns: 3fr 1.2fr;
  gap: 30px;
  margin-bottom: 50px;
}

.columna-principal-noticia {
  border-right: 1px solid #eee;
  padding-right: 30px;
}

.portal-fila-inferior {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 30px;

  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  padding-top: 20px;
  border-top: 1px solid #ddd;
  margin-bottom: 50px;
}

.portal-footer {
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px 30px;
  text-align: center;
  border-top: 1px solid #eee;
  color: #888;
  font-size: 0.9em;
}
</style>

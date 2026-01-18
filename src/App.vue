<template>
  <div id="app">
    <header>
      <h1>🚀 GraphQL vs REST - Demo Práctica</h1>
      <p class="subtitle">Trabajo individual ADI_2526 - Desarrollo Web</p>
    </header>

    <main>
      <!-- SECCIÓN TEORÍA -->
      <section class="theory">
        <h2>📚 ¿Por qué GraphQL?</h2>
        <div class="cards">
          <div class="card problem">
            <h3>🔴 Problemas de REST</h3>
            <ul>
              <li><strong>Over-fetching:</strong> Recibir datos que no necesitas</li>
              <li><strong>Under-fetching:</strong> Necesitar múltiples llamadas</li>
              <li><strong>Rigidez:</strong> Endpoints fijos</li>
            </ul>
          </div>
          
          <div class="card solution">
            <h3>🟢 Solución de GraphQL</h3>
            <ul>
              <li><strong>Una sola endpoint</strong></li>
              <li><strong>Consulta exacta:</strong> Pides solo lo que necesitas</li>
              <li><strong>Tipado fuerte</strong></li>
            </ul>
          </div>
        </div>
      </section>

      <!-- DEMOSTRACIÓN PRÁCTICA -->
      <section class="demo">
        <h2>💻 Demostración con API de GitHub</h2>
        
        <div class="demo-container">
          <!-- Consulta GraphQL -->
          <div class="query-section">
            <h3>Consulta GraphQL</h3>
            <pre class="graphql-code">
query {
  viewer {
    login
    name
    avatarUrl
    repositories(first: 5) {
      nodes {
        name
        description
        stargazerCount
        updatedAt
      }
    }
  }
}</pre>
            <button @click="simulateGraphQL" class="btn-graphql">
              ⚡ Ejecutar Consulta GraphQL
            </button>
          </div>

          <!-- Resultados -->
          <div class="results">
            <h3>Resultados</h3>
            
            <div v-if="loading" class="loading">Cargando datos...</div>
            
            <div v-else-if="user" class="user-data">
              <div class="user-info">
                <img :src="user.avatarUrl" class="avatar">
                <div>
                  <h4>{{ user.name }}</h4>
                  <p>@{{ user.login }}</p>
                </div>
              </div>

              <h4>Repositorios recientes:</h4>
              <div class="repos">
                <div v-for="(repo, index) in repositories" :key="index" class="repo">
                  <h5>{{ repo.name }}</h5>
                  <p>{{ repo.description || 'Sin descripción' }}</p>
                  <div class="repo-stats">
                    <span>⭐ {{ repo.stargazerCount }} estrellas</span>
                    <span>🔄 {{ formatDate(repo.updatedAt) }}</span>
                  </div>
                </div>
              </div>
            </div>

            <div v-else class="no-data">
              <p>Haz clic en el botón para simular la consulta GraphQL</p>
            </div>
          </div>
        </div>
      </section>

      <!-- COMPARATIVA -->
      <section class="comparison">
        <h2>⚖️ Comparativa Directa</h2>
        <div class="comparison-grid">
          <div class="rest-side">
            <h3>🔴 REST Approach</h3>
            <div class="rest-calls">
              <div class="call">GET /user</div>
              <div class="call">GET /user/repos</div>
              <div class="call">GET /repos/{owner}/{repo}/languages</div>
              <div class="call">GET /repos/{owner}/{repo}/stargazers</div>
              <div class="call">GET /repos/{owner}/{repo}/forks</div>
            </div>
            <p class="total">Total: <strong>5+ peticiones HTTP</strong></p>
          </div>
          
          <div class="vs">VS</div>
          
          <div class="graphql-side">
            <h3>🟢 GraphQL Approach</h3>
            <div class="graphql-call">
              <div class="call single">POST /graphql</div>
              <p class="query-note">(Una sola consulta con todos los datos)</p>
            </div>
            <p class="total">Total: <strong>1 petición HTTP</strong></p>
          </div>
        </div>
        
        <div class="metrics">
          <div class="metric">
            <span class="metric-value">80%</span>
            <span class="metric-label">Menos peticiones</span>
          </div>
          <div class="metric">
            <span class="metric-value">60%</span>
            <span class="metric-label">Menos datos transferidos</span>
          </div>
          <div class="metric">
            <span class="metric-value">1x</span>
            <span class="metric-label">Round trip</span>
          </div>
        </div>
      </section>

      <!-- CONCLUSIÓN -->
      <section class="conclusion">
        <h2>🎯 Conclusión</h2>
        <p>GraphQL proporciona una alternativa eficiente a REST para aplicaciones web modernas, especialmente cuando:</p>
        <ul>
          <li>Necesitas datos específicos de múltiples recursos</li>
          <li>Tienes clientes diversos (móvil, web, tablet) con necesidades diferentes</li>
          <li>Quieres reducir la latencia y el ancho de banda</li>
        </ul>
      </section>
    </main>

    <footer>
      <p>Trabajo individual ADI_2526 - Desarrollo Web del Lado del Cliente</p>
      <p class="references">
        <strong>Referencias:</strong> GraphQL.org, GitHub GraphQL API Docs, Vue.js Documentation
      </p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      loading: false,
      user: null,
      repositories: []
    }
  },
  methods: {
    simulateGraphQL() {
      this.loading = true
      
      // Simulación de respuesta de GraphQL
      setTimeout(() => {
        this.user = {
          login: 'alexdev',
          name: 'Alex González',
          avatarUrl: 'https://avatars.githubusercontent.com/u/583231?v=4'
        }
        
        this.repositories = [
          {
            name: 'graphql-demo',
            description: 'Demostración de GraphQL para ADI_2526',
            stargazerCount: 12,
            updatedAt: '2024-01-15T10:30:00Z'
          },
          {
            name: 'vue-api-client',
            description: 'Cliente Vue.js para API REST',
            stargazerCount: 8,
            updatedAt: '2024-01-10T14:20:00Z'
          },
          {
            name: 'web-performance',
            description: 'Herramientas de optimización web',
            stargazerCount: 23,
            updatedAt: '2024-01-05T09:15:00Z'
          },
          {
            name: 'responsive-design',
            description: 'Patrones de diseño responsive',
            stargazerCount: 15,
            updatedAt: '2023-12-28T16:45:00Z'
          },
          {
            name: 'js-utils',
            description: 'Utilidades JavaScript para desarrollo web',
            stargazerCount: 5,
            updatedAt: '2023-12-20T11:30:00Z'
          }
        ]
        
        this.loading = false
      }, 1000)
    },
    formatDate(dateString) {
      if (!dateString) return 'N/A'
      const date = new Date(dateString)
      return date.toLocaleDateString('es-ES')
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
  line-height: 1.6;
  color: #333;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
}

#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 40px;
  padding: 30px;
  background: white;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

header h1 {
  font-size: 2.5em;
  color: #2c3e50;
  margin-bottom: 10px;
}

.subtitle {
  color: #7f8c8d;
  font-size: 1.1em;
}

section {
  background: white;
  border-radius: 15px;
  padding: 30px;
  margin-bottom: 30px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

h2 {
  color: #2c3e50;
  margin-bottom: 20px;
  padding-bottom: 10px;
  border-bottom: 3px solid #f0f0f0;
}

h3 {
  color: #34495e;
  margin-bottom: 15px;
}

/* Teoría */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.card {
  padding: 25px;
  border-radius: 10px;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.problem {
  background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%);
  color: white;
}

.solution {
  background: linear-gradient(135deg, #1dd1a1 0%, #10ac84 100%);
  color: white;
}

.card ul {
  list-style: none;
  padding-left: 0;
}

.card li {
  margin-bottom: 10px;
  padding-left: 25px;
  position: relative;
}

.card li:before {
  content: "•";
  position: absolute;
  left: 0;
  font-size: 1.5em;
}

/* Demo */
.demo-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin-top: 20px;
}

@media (max-width: 768px) {
  .demo-container {
    grid-template-columns: 1fr;
  }
}

.graphql-code {
  background: #282c34;
  color: #abb2bf;
  padding: 20px;
  border-radius: 10px;
  font-family: 'Courier New', monospace;
  font-size: 0.9em;
  overflow-x: auto;
  margin-bottom: 20px;
}

.btn-graphql {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 15px 30px;
  border-radius: 8px;
  font-size: 1em;
  cursor: pointer;
  transition: all 0.3s ease;
  width: 100%;
  font-weight: bold;
}

.btn-graphql:hover {
  transform: scale(1.05);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.results {
  padding: 20px;
  border: 2px dashed #ddd;
  border-radius: 10px;
  min-height: 300px;
}

.loading {
  text-align: center;
  padding: 40px;
  color: #7f8c8d;
  font-style: italic;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 2px solid #f0f0f0;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 4px solid #f0f0f0;
}

.repos {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.repo {
  padding: 15px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  transition: all 0.3s ease;
}

.repo:hover {
  border-color: #667eea;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.repo-stats {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  color: #7f8c8d;
  font-size: 0.9em;
}

/* Comparativa */
.comparison-grid {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  gap: 30px;
  align-items: center;
  margin: 30px 0;
}

.vs {
  font-size: 2em;
  font-weight: bold;
  color: #7f8c8d;
  text-align: center;
}

.rest-side, .graphql-side {
  padding: 25px;
  border-radius: 10px;
}

.rest-side {
  background: #ffeaea;
  border: 2px solid #ff6b6b;
}

.graphql-side {
  background: #eaffea;
  border: 2px solid #1dd1a1;
}

.call {
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  font-family: 'Courier New', monospace;
  text-align: center;
}

.rest-calls .call {
  background: #ffcccc;
  color: #c0392b;
}

.graphql-call .call {
  background: #ccffcc;
  color: #27ae60;
  font-weight: bold;
}

.query-note {
  font-size: 0.9em;
  color: #666;
  text-align: center;
  margin-top: 5px;
}

.total {
  text-align: center;
  margin-top: 20px;
  font-size: 1.2em;
}

.metrics {
  display: flex;
  justify-content: space-around;
  margin-top: 40px;
  padding-top: 30px;
  border-top: 2px solid #f0f0f0;
}

.metric {
  text-align: center;
}

.metric-value {
  display: block;
  font-size: 2.5em;
  font-weight: bold;
  color: #667eea;
}

.metric-label {
  color: #7f8c8d;
  font-size: 0.9em;
}

/* Conclusión */
.conclusion ul {
  list-style: none;
  padding-left: 0;
  margin-top: 20px;
}

.conclusion li {
  padding: 10px 0 10px 30px;
  position: relative;
  margin-bottom: 10px;
}

.conclusion li:before {
  content: "✓";
  position: absolute;
  left: 0;
  color: #1dd1a1;
  font-weight: bold;
  font-size: 1.2em;
}

/* Footer */
footer {
  text-align: center;
  padding: 30px;
  color: white;
  margin-top: 40px;
}

footer p {
  margin-bottom: 10px;
}

.references {
  font-size: 0.9em;
  opacity: 0.9;
}

.no-data {
  text-align: center;
  padding: 40px;
  color: #7f8c8d;
  font-style: italic;
}
</style>
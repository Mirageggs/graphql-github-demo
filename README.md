# 🚀 GraphQL vs REST - Trabajo ADI_2526

### 🎯 CÓMO FUNCIONA LA APLICACIÓN
1. **Al abrir**: Explicación teórica con colores diferenciados
2. **Al hacer clic en "Ejecutar Consulta GraphQL"**: 
   - Simula una petición GraphQL a la API de GitHub
   - Muestra datos de usuario (nombre, avatar, bio)
   - Muestra 5 repositorios con estrellas y fechas
3. **Sección comparativa**: Muestra visualmente la diferencia

### 📊 MÉTRICAS DEMOSTRADAS
| Enfoque | Peticiones | Datos Transferidos | Tiempo |
|---------|------------|-------------------|--------|
| REST | 5+ | ~50KB | Múltiples round-trips |
| GraphQL | 1 | ~20KB | 1 round-trip |

### 🛠️ CÓDIGO CLAVE
```javascript
// Método que simula la consulta GraphQL
simulateGraphQL() {
  this.loading = true
  setTimeout(() => {
    this.user = { login: 'alexdev', name: 'Alex González' }
    this.repositories = [...]
    this.loading = false
  }, 1000)
}

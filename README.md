# TrunkBasedDevelopment_Workflow

> Trunk Based Development es una estrategia que se basa en que el mayor tiempo de desarrollo se concentra en una sola rama llamada trunk.

![](images/TrunkBasedDevelopment.png)

Trunk Based Development (TBD) es una estrategia de desarrollo de software que se enfoca en mantener un único branch (rama) principal, llamada "trunk" o "main", donde los desarrolladores integran sus cambios con frecuencia. A diferencia de otros modelos como GitFlow, donde las ramas pueden ser largas y ramificadas, TBD promueve una integración continua y rápida en una sola línea de desarrollo. Aquí hay una explicación detallada del flujo de trabajo de TBD:

### Principios de Trunk Based Development

1. **Integración Frecuente**
   - Los desarrolladores realizan integraciones de código al trunk varias veces al día. Esto asegura que los cambios sean pequeños y manejables, lo que facilita la identificación y resolución de conflictos.

2. **Ramas de Vida Corta**
   - Si se utilizan ramas (features branches), estas son de vida corta, típicamente de un par de días como máximo. Una vez completada una característica o arreglo, se integran rápidamente al trunk.

3. **Feature Flags**
   - Las nuevas características se integran al trunk bajo control de feature flags (banderas de características), permitiendo que el código se despliegue en producción sin activar la nueva funcionalidad hasta que esté completamente lista.

4. **Automatización de Pruebas y CI/CD**
   - Las pruebas automáticas y la integración continua son esenciales. Cada cambio integrado en el trunk dispara una serie de pruebas automatizadas para asegurar que no se rompa la estabilidad del trunk.

### Flujo de Trabajo en Trunk Based Development

#### 1. **Desarrollo en el Trunk**
   - Todos los desarrolladores trabajan directamente en el trunk, realizando commits frecuentes.

   ```sh
   git checkout main
   git pull origin main
   # Realizar cambios
   git add .
   git commit -m "Descripción del cambio"
   git push origin main
   ```

#### 2. **Uso de Feature Flags**
   - Implementar características detrás de feature flags permite que el código incompleto se integre y despliegue sin afectar a los usuarios finales.

   ```javascript
   if (featureFlag.isEnabled("nueva-funcionalidad")) {
       // Código para la nueva funcionalidad
   }
   ```

#### 3. **Ramas de Vida Corta (Opcional)**
   - En caso de que se necesiten ramas, se crean ramas cortas para trabajar en características específicas y se integran rápidamente al trunk.

   ```sh
   git checkout -b feature/nueva-funcionalidad
   # Realizar cambios
   git add .
   git commit -m "Descripción del cambio"
   git checkout main
   git pull origin main
   git merge feature/nueva-funcionalidad
   git push origin main
   ```

#### 4. **Integración Continua y Pruebas Automatizadas**
   - Cada push al trunk desencadena un pipeline de CI que ejecuta pruebas automatizadas para verificar la estabilidad del código.

   ```yaml
   # Ejemplo de configuración de CI en un archivo YAML
   steps:
     - name: Checkout code
       uses: actions/checkout@v2
     - name: Run tests
       run: npm test
   ```

### Beneficios de Trunk Based Development

- **Menos Conflictos de Integración**: Al integrar cambios con frecuencia, los conflictos son menores y más fáciles de resolver.
- **Mayor Velocidad de Entrega**: Los ciclos de entrega son más rápidos debido a la integración continua.
- **Mayor Calidad del Código**: Las pruebas continuas aseguran que el código en el trunk esté siempre en un estado desplegable.
- **Mejor Colaboración**: Fomenta una cultura de colaboración y comunicación continua entre los desarrolladores.

### Desafíos de Trunk Based Development

- **Disciplina en Pruebas y CI**: Requiere una sólida disciplina en la escritura de pruebas y la configuración de pipelines de CI.
- **Gestión de Feature Flags**: La correcta gestión de feature flags es crucial para evitar complicaciones en el código.
- **Adaptación Cultural**: Puede requerir un cambio cultural en equipos acostumbrados a trabajar con ramas largas y múltiples.

### Ejemplo de Ciclo Completo en TBD

1. **Sincronización con el trunk**: `git checkout main && git pull origin main`
2. **Desarrollo de la característica**: `git checkout -b feature/nueva-funcionalidad`
3. **Realizar cambios y commits**:
   ```sh
   git add .
   git commit -m "Añadida nueva funcionalidad detrás de una feature flag"
   ```
4. **Merge rápido al trunk**:
   ```sh
   git checkout main
   git pull origin main
   git merge feature/nueva-funcionalidad
   git push origin main
   ```
5. **Despliegue y activación de la feature flag cuando esté lista**.

Este flujo asegura un desarrollo ágil y continuo, con un enfoque en la estabilidad y la entrega rápida de software.

I'll explore the project structure to understand what it is and then explain how to use it for your own projects.

# ¿Qué es Maestro?

**Maestro** es una extensión para Gemini CLI que transforma la herramienta en una plataforma de orquestación multi-agente. En lugar de que una sola IA sesgada haga todo, Maestro delega el trabajo a **12 agentes especializados**, cada uno con su propio contexto, herramientas y experiencia.

## Arquitectura Principal

### 4 Fases de Workflow:
1. **Design** - Diálogo estructurado para entender requisitos
2. **Plan** - Ensamblaje del equipo y planificación detallada 
3. **Execute** - Ejecución paralela o secuencial de fases
4. **Complete** - Revisión final y archivado

### Los 12 Agentes Especializados:
- **architect** - Diseño de sistemas y selección de tecnología
- **coder** - Implementación de funcionalidades
- **tester** - Pruebas unitarias/integración/E2E
- **code_reviewer** - Revisión de calidad y mejores prácticas
- **debugger** - Análisis de causa raíz
- **security_engineer** - Evaluación de vulnerabilidades
- **performance_engineer** - Optimización y profiling
- **data_engineer** - Diseño de esquemas y ETL
- **devops_engineer** - CI/CD e infraestructura
- **api_designer** - Diseño de APIs REST/GraphQL
- **technical_writer** - Documentación técnica
- **refactor** - Modernización de código

## ¿Cómo Usarlo para Tus Proyectos?

### 1. Instalación
```bash
# Habilitar agentes experimentales en Gemini CLI
# Editar ~/.gemini/settings.json:
{
  "experimental": {
    "enableAgents": true
  }
}

# Instalar Maestro
gemini extensions install https://github.com/josstei/maestro-gemini
```

### 2. Comandos Principales

#### Orquestación Completa:
```
/maestro:orchestrate Build a REST API for task management with auth
```
Inicia el workflow completo: diseño → planificación → ejecución → completado

#### Ejecutar Plan Existente:
```
/maestro:execute path/to/plan.md
```
Salta las fases de diseño y va directo a la ejecución

#### Reanudar Sesión:
```
/maestro:resume
```
Continúa desde donde se quedó una sesión interrumpida

#### Herramientas Independientes:
```
/maestro:review [archivos]           # Revisión de código
/maestro:debug <descripción>         # Debugging
/maestro:security-audit <ámbito>     # Auditoría de seguridad
/maestro:perf-check <ámbito>         # Análisis de rendimiento
```

### 3. Flujo de Trabajo Típico

1. **Inicio**: `/maestro:orchestrate <tu proyecto>`
2. **Diálogo de Diseño**: Maestro hace preguntas estructuradas sobre tus requisitos
3. **Propuestas Arquitectónicas**: Te presenta 2-3 enfoques con pros/contras
4. **Planificación**: Asigna agentes a fases específicas
5. **Ejecución**: Los agentes trabajan (paralelo cuando es posible)
6. **Revisión Final**: Code reviewer valida la calidad

### 4. Estado y Archivos

Maestro crea un directorio `.gemini/` en tu proyecto:
- `state/active-session.md` - Estado actual de la orquestación
- `plans/` - Documentos de diseño y planes de implementación
- `parallel/` - Resultados de ejecución paralela
- `archive/` - Sesiones completadas

## Casos de Uso para Tus Proyectos

### **Proyecto Nuevo**:
```
/maestro:orchestrate Create a React app with TypeScript, authentication, and PostgreSQL backend
```

### **Mejora Existente**:
```
/maestro:orchestrate Add microservices architecture to existing monolith app
```

### **Debugging**:
```
/maestro:debug API endpoints returning 500 errors in production
```

### **Revisión de Calidad**:
```
/maestro:review src/ components/
```

### **Optimización**:
```
/maestro:perf-check Database queries are slow
```

## Configuración Clave

Variables de entorno importantes:
- `MAESTRO_STATE_DIR` - Directorio para estado (default: `.gemini`)
- `MAESTRO_EXECUTION_MODE` - `parallel`/`sequential`/`ask`
- `MAESTRO_AGENT_TIMEOUT` - Timeout por agente (default: 10 min)
- `MAESTRO_MAX_CONCURRENT` - Máximo agentes en paralelo

## Ventajas para Desarrollo

1. **Especialización** - Cada agente es experto en su dominio
2. **Paralelización** - Fases independentes ejecutan concurrentemente
3. **Persistencia** - Todo el estado se guarda para reanudar
4. **Calidad** - Múltiples capas de revisión automática
5. **Flexibilidad** - Puedes usar orquestación completa o herramientas individuales

Maestro es ideal para proyectos complejos donde necesitas múltiples especialidades (backend, frontend, testing, DevOps) y quieres un proceso estructurado con calidad garantizada.
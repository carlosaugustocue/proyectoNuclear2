# Sistema de Gestión Clínica Veterinaria (GCV)

## 📋 Descripción del Proyecto

Sistema integral de gestión para clínicas veterinarias que permite administrar pacientes, citas, historiales clínicos, inventario, facturación y seguimiento de clientes. El sistema está diseñado para facilitar las operaciones diarias de una clínica veterinaria y mejorar la atención a los pacientes.

## 🎯 Objetivos

- Centralizar la información de pacientes (mascotas) y clientes
- Optimizar la gestión de citas y agenda de veterinarios
- Mantener historiales clínicos completos y organizados
- Controlar el inventario de medicamentos e insumos
- Automatizar la facturación y control financiero
- Mejorar la comunicación y seguimiento con los clientes

## 📚 Documentación de Requisitos

Este repositorio contiene la documentación completa de historias de usuario para el sistema:

### Archivos Incluidos

- **`historias_usuario_gcv.md`**: Documento completo con 11 historias de usuario en formato Markdown, incluyendo criterios de aceptación detallados, prioridades y estimaciones en Story Points.

- **`historias_usuario_import.csv`**: Archivo CSV listo para importar en sistemas de gestión de proyectos (Jira, Azure DevOps, etc.) con todas las historias de usuario estructuradas.

## 🔧 Historias de Usuario

El proyecto contempla **11 historias de usuario principales** con un total de **110 Story Points**:

### Prioridad Alta (81 Story Points)

1. **HU-01: Gestión de Usuarios** (8 SP) - Control de acceso, roles y permisos
2. **HU-02: Gestión de Pacientes** (13 SP) - Registro y seguimiento de mascotas
3. **HU-03: Gestión de Citas** (13 SP) - Programación y agenda de veterinarios
4. **HU-04: Inventario** (8 SP) - Control de medicamentos e insumos
5. **HU-05: Facturación** (13 SP) - Generación de facturas y control financiero
6. **HU-06: Historial Clínico** (13 SP) - Expediente médico completo
7. **HU-07: Prestación de Servicios** (13 SP) - Registro de consultas y procedimientos

### Prioridad Media (29 Story Points)

8. **HU-08: Configuración del Sistema** (8 SP) - Parametrización general
9. **HU-09: Tipos de Mascotas** (5 SP) - Catálogo de especies y razas
10. **HU-10: Seguimiento Cliente** (8 SP) - CRM y fidelización
11. **HU-11: Triage** (8 SP) - Evaluación inicial y priorización

## 👥 Roles del Sistema

- **Administrador**: Gestión completa del sistema, usuarios y configuración
- **Veterinario**: Atención médica, historiales clínicos, servicios
- **Recepcionista**: Gestión de citas, pacientes, facturación
- **Asistente**: Triage, apoyo en consultas

## 🚀 Características Principales

- ✅ Gestión completa de pacientes y propietarios
- ✅ Sistema de citas con recordatorios automáticos
- ✅ Historial clínico digital con adjuntos
- ✅ Control de inventario con alertas de stock
- ✅ Facturación y reportes financieros
- ✅ Sistema de triage para priorización
- ✅ Seguimiento y fidelización de clientes
- ✅ Configuración flexible y personalizable
- ✅ Control de acceso basado en roles
- ✅ Auditoría de cambios

## 📊 Importar Historias a Herramientas de Gestión

### Para Jira

1. Ve a **Proyecto > Importar**
2. Selecciona **CSV**
3. Carga el archivo `historias_usuario_import.csv`
4. Mapea los campos correctamente
5. Completa la importación

### Para Azure DevOps

1. Ve a **Boards > Work Items**
2. Selecciona **Import Work Items**
3. Carga el archivo `historias_usuario_import.csv`
4. Revisa y confirma la importación

## 📖 Formato de Historias de Usuario

Cada historia sigue el formato estándar:

```
Como [rol]
Quiero [funcionalidad]
Para [beneficio]

Criterios de Aceptación:
- [Criterio 1]
- [Criterio 2]
- ...
```

## 🏗️ Planificación Sugerida

### Sprint 1 (Prioridad Alta - Fase 1)
- HU-01: Gestión de Usuarios
- HU-02: Gestión de Pacientes
- HU-09: Tipos de Mascotas

### Sprint 2 (Prioridad Alta - Fase 2)
- HU-03: Gestión de Citas
- HU-04: Inventario

### Sprint 3 (Prioridad Alta - Fase 3)
- HU-06: Historial Clínico
- HU-07: Prestación de Servicios

### Sprint 4 (Prioridad Alta - Fase 4)
- HU-05: Facturación

### Sprint 5 (Prioridad Media)
- HU-08: Configuración del Sistema
- HU-10: Seguimiento Cliente
- HU-11: Triage

## 🛠️ Tecnologías Sugeridas

*Pendiente de definir según decisiones del equipo técnico*

Posibles tecnologías:
- Backend: Java/Spring Boot, Node.js, .NET
- Frontend: React, Angular, Vue.js
- Base de datos: PostgreSQL, MySQL, MongoDB
- Arquitectura: Microservicios / Monolito modular

## 📝 Contribución

Este documento está en desarrollo continuo. Antes de cada sprint, se recomienda:

1. Revisar y refinar las historias de usuario con el equipo
2. Validar los criterios de aceptación con stakeholders
3. Ajustar las estimaciones según la velocidad del equipo
4. Definir las pruebas de aceptación específicas

## 📄 Licencia

*Pendiente de definir*

## 👨‍💻 Equipo

*Pendiente de definir*

---

**Última actualización**: Octubre 2024  
**Versión**: 1.0  
**Estado**: Documentación de Requisitos

# Historias de Usuario - Gestión Clínica Veterinaria (GCV)

---

## HU-01: Gestión de Usuarios

**Como** administrador del sistema  
**Quiero** gestionar los usuarios del sistema (crear, editar, eliminar y asignar roles)  
**Para** controlar el acceso y los permisos de cada miembro del equipo

**Criterios de Aceptación:**
- El sistema permite crear nuevos usuarios con información básica (nombre, email, contraseña, rol)
- Se pueden asignar roles específicos: Administrador, Veterinario, Recepcionista, Asistente
- Es posible editar la información de usuarios existentes
- Se puede desactivar o eliminar usuarios del sistema
- Los usuarios solo pueden acceder a funcionalidades permitidas según su rol
- El sistema valida que el email sea único
- Las contraseñas deben cumplir requisitos de seguridad (mínimo 8 caracteres, mayúsculas, números)
- Se registra un log de auditoría de cambios en usuarios

**Prioridad:** Alta  
**Estimación:** 8 Story Points

---

## HU-02: Gestión de Pacientes

**Como** recepcionista o veterinario  
**Quiero** registrar y mantener actualizada la información de los pacientes (mascotas)  
**Para** tener un registro completo y organizado de cada animal

**Criterios de Aceptación:**
- Se puede registrar un nuevo paciente con: nombre, especie, raza, fecha de nacimiento, sexo, color, peso
- Cada paciente está vinculado a un propietario (cliente)
- Es posible editar la información del paciente en cualquier momento
- Se puede buscar pacientes por nombre, especie, o propietario
- El sistema permite adjuntar fotos del paciente
- Se muestra el historial resumido del paciente (última visita, próxima cita, estado)
- Se puede marcar pacientes como inactivos o fallecidos
- Se valida que los campos obligatorios estén completos

**Prioridad:** Alta  
**Estimación:** 13 Story Points

---

## HU-03: Gestión de Citas

**Como** recepcionista  
**Quiero** programar, reagendar y cancelar citas para los pacientes  
**Para** organizar eficientemente la agenda de los veterinarios

**Criterios de Aceptación:**
- Se puede crear una cita seleccionando: fecha, hora, paciente, veterinario, tipo de servicio y motivo
- El sistema muestra la disponibilidad del veterinario en tiempo real
- Es posible reagendar una cita existente
- Se puede cancelar una cita con registro del motivo
- El sistema envía recordatorios automáticos al cliente (24 horas antes)
- Se visualiza la agenda diaria, semanal y mensual
- Se pueden filtrar citas por estado: Programada, En curso, Completada, Cancelada
- El sistema alerta sobre conflictos de horario
- Se permite agregar notas adicionales a la cita

**Prioridad:** Alta  
**Estimación:** 13 Story Points

---

## HU-04: Inventario

**Como** veterinario o administrador  
**Quiero** gestionar el inventario de medicamentos, insumos y productos  
**Para** mantener un control adecuado del stock y evitar desabastecimientos

**Criterios de Aceptación:**
- Se pueden registrar productos con: nombre, código, categoría, cantidad, precio, fecha de vencimiento
- El sistema actualiza automáticamente el stock cuando se utiliza o vende un producto
- Se generan alertas cuando un producto alcanza el stock mínimo
- Se pueden realizar ajustes de inventario con justificación
- Es posible generar reportes de movimientos de inventario
- Se muestran alertas de productos próximos a vencer (30 días antes)
- Se puede buscar productos por nombre, código o categoría
- El sistema registra el historial de movimientos por producto

**Prioridad:** Alta  
**Estimación:** 8 Story Points

---

## HU-05: Facturación

**Como** recepcionista o administrador  
**Quiero** generar facturas por los servicios y productos vendidos  
**Para** llevar un control financiero de la clínica

**Criterios de Aceptación:**
- Se puede crear una factura seleccionando servicios prestados y productos vendidos
- La factura se asocia automáticamente a un cliente y paciente
- El sistema calcula automáticamente subtotales, descuentos, impuestos y total
- Es posible aplicar descuentos por porcentaje o monto fijo
- Se pueden imprimir o enviar facturas por email en formato PDF
- El sistema registra el método de pago (efectivo, tarjeta, transferencia)
- Se puede consultar el historial de facturas por cliente o fecha
- Es posible anular facturas con registro de motivo
- Se generan reportes de ventas diarias, mensuales y anuales

**Prioridad:** Alta  
**Estimación:** 13 Story Points

---

## HU-06: Historial Clínico

**Como** veterinario  
**Quiero** registrar y consultar el historial clínico completo de cada paciente  
**Para** brindar una atención médica informada y dar seguimiento a tratamientos

**Criterios de Aceptación:**
- Se puede crear una entrada de historial médico con: fecha, motivo, diagnóstico, tratamiento, observaciones
- Cada entrada se vincula a una consulta o visita específica
- Es posible registrar signos vitales (temperatura, peso, frecuencia cardíaca, frecuencia respiratoria)
- Se pueden adjuntar archivos (radiografías, análisis de laboratorio, imágenes)
- El sistema muestra el historial cronológico completo del paciente
- Solo veterinarios autorizados pueden crear y editar entradas médicas
- Se puede generar un reporte PDF del historial completo
- El historial incluye vacunas, desparasitaciones y cirugías realizadas

**Prioridad:** Alta  
**Estimación:** 13 Story Points

---

## HU-07: Prestación de Servicios y Consulta

**Como** veterinario  
**Quiero** registrar los servicios prestados durante una consulta o procedimiento  
**Para** documentar el trabajo realizado y generar los cobros correspondientes

**Criterios de Aceptación:**
- Se puede iniciar una consulta desde una cita programada
- El sistema permite seleccionar múltiples servicios de un catálogo predefinido
- Se pueden agregar servicios personalizados con descripción y precio
- Cada servicio se registra con fecha, hora, veterinario responsable y observaciones
- Los servicios se vinculan automáticamente al historial del paciente
- Se puede prescribir medicamentos que se descuentan automáticamente del inventario
- El sistema calcula el costo total de los servicios prestados
- Los servicios registrados se pueden facturar directamente
- Se registra el tiempo de inicio y fin de la consulta

**Prioridad:** Alta  
**Estimación:** 13 Story Points

---

## HU-08: Configuración del Sistema

**Como** administrador  
**Quiero** configurar parámetros generales del sistema  
**Para** personalizar el funcionamiento según las necesidades de la clínica

**Criterios de Aceptación:**
- Se pueden configurar datos de la clínica (nombre, dirección, teléfono, logo)
- Es posible definir horarios de atención por día de la semana
- Se pueden configurar tipos de servicios con precios base
- El sistema permite personalizar categorías de productos para inventario
- Se puede configurar el formato de facturas y documentos
- Es posible definir niveles de stock mínimo por categoría
- Se pueden establecer porcentajes de impuestos aplicables
- El sistema permite configurar notificaciones por email y SMS
- Se puede definir la duración estándar de las citas por tipo de servicio

**Prioridad:** Media  
**Estimación:** 8 Story Points

---

## HU-09: Tipos de Mascotas

**Como** administrador o recepcionista  
**Quiero** gestionar un catálogo de tipos de mascotas (especies y razas)  
**Para** estandarizar la información al registrar pacientes

**Criterios de Aceptación:**
- Se puede crear, editar y eliminar especies (perro, gato, ave, reptil, etc.)
- Para cada especie se pueden definir múltiples razas
- El sistema incluye un catálogo predefinido de especies y razas comunes
- Es posible agregar razas personalizadas o "mestizo"
- Al registrar un paciente, se selecciona especie y raza de listas desplegables
- El sistema permite buscar y filtrar pacientes por tipo de mascota
- Se pueden generar estadísticas por especie y raza
- Las razas obsoletas se pueden desactivar sin eliminar registros históricos

**Prioridad:** Media  
**Estimación:** 5 Story Points

---

## HU-10: Seguimiento Cliente

**Como** recepcionista o veterinario  
**Quiero** hacer seguimiento a los clientes y sus mascotas  
**Para** mantener una comunicación proactiva y mejorar la fidelización

**Criterios de Aceptación:**
- El sistema registra todas las interacciones con el cliente (llamadas, emails, mensajes)
- Se pueden programar recordatorios de seguimiento con fecha y descripción
- El sistema envía notificaciones automáticas de recordatorios pendientes
- Es posible registrar quejas, sugerencias o felicitaciones del cliente
- Se visualiza un timeline de todas las interacciones del cliente
- El sistema alerta sobre clientes inactivos (sin citas en los últimos 6 meses)
- Se pueden enviar mensajes masivos para campañas de vacunación o promociones
- Se registra el nivel de satisfacción del cliente después de cada servicio
- Es posible clasificar clientes por segmentos (VIP, frecuente, ocasional)

**Prioridad:** Media  
**Estimación:** 8 Story Points

---

## HU-11: Triage

**Como** asistente veterinario o enfermero  
**Quiero** realizar una evaluación inicial (triage) de los pacientes  
**Para** priorizar la atención según la urgencia del caso

**Criterios de Aceptación:**
- Se puede realizar triage al momento que llega el paciente a la clínica
- El sistema permite registrar: motivo de consulta, signos vitales básicos, síntomas observables
- Se asigna un nivel de prioridad: Crítico, Urgente, Moderado, No urgente
- El nivel de prioridad es visible en la lista de espera y agenda
- Los casos críticos se destacan visualmente con alertas
- Se puede reasignar la prioridad si cambia la condición del paciente
- El veterinario puede ver la información del triage antes de la consulta
- El sistema registra el tiempo de espera desde el triage hasta la atención
- Se generan reportes de tiempos de atención por nivel de prioridad

**Prioridad:** Media  
**Estimación:** 8 Story Points

---

## Resumen de Estimaciones

| Historia de Usuario | Story Points | Prioridad |
|---------------------|--------------|-----------|
| HU-01: Gestión de Usuarios | 8 | Alta |
| HU-02: Gestión de Pacientes | 13 | Alta |
| HU-03: Gestión de Citas | 13 | Alta |
| HU-04: Inventario | 8 | Alta |
| HU-05: Facturación | 13 | Alta |
| HU-06: Historial Clínico | 13 | Alta |
| HU-07: Prestación de Servicios | 13 | Alta |
| HU-08: Configuración del Sistema | 8 | Media |
| HU-09: Tipos de Mascotas | 5 | Media |
| HU-10: Seguimiento Cliente | 8 | Media |
| HU-11: Triage | 8 | Media |
| **TOTAL** | **110** | - |

---

## Notas Adicionales

- Estas historias de usuario siguen el formato estándar: Como [rol] Quiero [funcionalidad] Para [beneficio]
- Los Story Points están estimados considerando complejidad, esfuerzo y riesgo
- Se recomienda priorizar las historias de "Alta" prioridad en el primer sprint
- Cada historia debe ser revisada y refinada con el equipo antes de implementación
- Los criterios de aceptación deben ser verificados mediante pruebas antes de marcar como completa

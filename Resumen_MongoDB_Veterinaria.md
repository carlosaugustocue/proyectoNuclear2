# Diseño de Base de Datos MongoDB - Sistema de Gestión Veterinaria

**Proyecto Nuclear - Bases de Datos 2**  
**Fecha:** 25 de Octubre de 2025

---

## 📋 Resumen Ejecutivo

Este documento presenta el diseño completo de la base de datos MongoDB para el Sistema de Gestión Veterinaria, basado en el diagrama de clases proporcionado.

### Colecciones Principales

1. **usuarios** - Todos los tipos de usuarios con discriminador de rol
2. **mascotas** - Mascotas con historia clínica embebida
3. **citas** - Agendamiento de servicios veterinarios
4. **facturas** - Documentos de facturación con detalles y pagos
5. **productos** - Medicamentos e insumos con control de inventario
6. **proveedores** - Proveedores de productos
7. **notificaciones** - Sistema de notificaciones y alertas

---

## 🎯 Decisiones de Diseño Clave

### Embedding vs Referencing

**Embebido (Embedded):**
- Historia clínica dentro de mascotas (relación 1:1, siempre se consultan juntos)
- Detalles de factura (no cambian después de emisión)
- Pagos dentro de facturas (pocos pagos por factura)
- Movimientos recientes de inventario (limitados a últimos 10)

**Referencias (Referencing):**
- Propietario → Mascotas (1:N)
- Cliente → Citas (N:N)
- Veterinario → Citas (N:N)
- Mascota → Citas (N:N)
- Proveedor → Productos (N:N)

**Desnormalización Estratégica:**
- Nombres de propietarios en mascotas
- Nombres de clientes y veterinarios en citas
- Nombres de proveedores en productos

---

## 🚀 Comandos de Creación

### 1. Crear Base de Datos

```javascript
// Conectarse a MongoDB
mongosh

// Crear y usar la base de datos
use veterinaria_db
```

### 2. Colección: usuarios

```javascript
// Crear colección con validación
db.createCollection('usuarios', {
  validator: {
    $jsonSchema: {
      bsonType: 'object',
      required: ['email', 'passwordHash', 'nombre', 'rol', 'tipoUsuario'],
      properties: {
        email: { bsonType: 'string', pattern: '^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$' },
        rol: { enum: ['CLIENTE', 'VETERINARIO', 'RECEPCIONISTA', 'ADMINISTRADOR'] },
        tipoUsuario: { enum: ['Cliente', 'Veterinario', 'Recepcionista', 'Administrador'] }
      }
    }
  }
});

// Crear índices
db.usuarios.createIndex({ email: 1 }, { unique: true });
db.usuarios.createIndex({ rol: 1 });
db.usuarios.createIndex({ tipoUsuario: 1 });

// Documento de ejemplo - Cliente
db.usuarios.insertOne({
  email: "maria.garcia@email.com",
  passwordHash: "$2b$10$abc123...",
  nombre: "María García",
  telefono: "+57 310 456 7890",
  rol: "CLIENTE",
  tipoUsuario: "Cliente",
  fechaCreacion: new Date(),
  activo: true,
  direccion: "Carrera 15 #20-30, Bogotá",
  documentoIdentidad: "1098765432"
});

// Documento de ejemplo - Veterinario
db.usuarios.insertOne({
  email: "dr.rodriguez@veterinaria.com",
  passwordHash: "$2b$10$xyz789...",
  nombre: "Dr. Carlos Rodríguez",
  telefono: "+57 315 789 0123",
  rol: "VETERINARIO",
  tipoUsuario: "Veterinario",
  fechaCreacion: new Date(),
  activo: true,
  especialidad: "Cirugía y Ortopedia",
  licenciaProfesional: "MV-54321"
});
```

### 3. Colección: mascotas

```javascript
db.createCollection('mascotas');

// Índices
db.mascotas.createIndex({ propietarioId: 1 });
db.mascotas.createIndex({ nombre: 1 });
db.mascotas.createIndex({ especie: 1 });
db.mascotas.createIndex({ 'historiaClinica.diagnosticos.codigoPatologia': 1 });

// Documento de ejemplo
db.mascotas.insertOne({
  nombre: "Max",
  especie: "Canino",
  raza: "Golden Retriever",
  fechaNacimiento: new Date("2020-03-15"),
  sexo: "Macho",
  estadoActual: "Saludable",
  propietarioId: ObjectId("..."),
  propietarioNombre: "María García",
  historiaClinica: {
    fechaApertura: new Date("2020-04-01"),
    resumen: "Mascota saludable, vacunación al día",
    evoluciones: [
      {
        evolucionId: new ObjectId(),
        fecha: new Date("2024-10-20"),
        nota: "Control de rutina. Se observa buen estado general.",
        veterinarioId: ObjectId("..."),
        veterinarioNombre: "Dr. Carlos Rodríguez"
      }
    ],
    diagnosticos: [
      {
        diagnosticoId: new ObjectId(),
        fecha: new Date("2023-06-10"),
        codigoPatologia: "K81.0",
        descripcion: "Gastritis leve"
      }
    ],
    documentos: [
      {
        documentoId: new ObjectId(),
        nombreArchivo: "radiografia_20241020.pdf",
        ruta: "/documentos/mascotas/max_radiografia.pdf",
        fechaSubida: new Date("2024-10-20"),
        tipo: "radiografia"
      }
    ]
  }
});
```

### 4. Colección: citas

```javascript
db.createCollection('citas');

// Índices
db.citas.createIndex({ fechaHora: 1 });
db.citas.createIndex({ mascotaId: 1 });
db.citas.createIndex({ clienteId: 1 });
db.citas.createIndex({ veterinarioId: 1, fechaHora: 1 });
db.citas.createIndex({ estado: 1 });

// Documento de ejemplo
db.citas.insertOne({
  fechaHora: new Date("2024-10-28T14:00:00Z"),
  tipoServicio: "consulta",
  estado: "CONFIRMADA",
  motivo: "Control de rutina y vacunación anual",
  duracionMin: 30,
  mascotaId: ObjectId("..."),
  mascotaNombre: "Max",
  clienteId: ObjectId("..."),
  clienteNombre: "María García",
  clienteTelefono: "+57 310 456 7890",
  veterinarioId: ObjectId("..."),
  veterinarioNombre: "Dr. Carlos Rodríguez",
  fechaCreacion: new Date(),
  notificacionesEnviadas: { notif24h: false, notif1h: false }
});
```

### 5. Colección: facturas

```javascript
db.createCollection('facturas');

// Índices
db.facturas.createIndex({ numeroFactura: 1 }, { unique: true });
db.facturas.createIndex({ clienteId: 1 });
db.facturas.createIndex({ citaId: 1 });
db.facturas.createIndex({ fechaEmision: -1 });
db.facturas.createIndex({ estado: 1 });

// Documento de ejemplo
db.facturas.insertOne({
  numeroFactura: "FAC-2024-001234",
  fechaEmision: new Date(),
  citaId: ObjectId("..."),
  clienteId: ObjectId("..."),
  clienteNombre: "María García",
  clienteDocumento: "1098765432",
  detalles: [
    { descripcion: "Consulta Veterinaria", cantidad: 1, precioUnitario: 80000, subtotal: 80000 },
    { descripcion: "Vacuna Antirrábica", cantidad: 1, precioUnitario: 45000, subtotal: 45000 }
  ],
  totalBruto: 125000,
  descuento: 0,
  totalNeto: 125000,
  estado: "PAGADA",
  pagos: [
    {
      pagoId: new ObjectId(),
      fechaPago: new Date(),
      monto: 125000,
      metodo: "tarjeta_credito",
      referencia: "VISA-****1234"
    }
  ]
});
```

### 6. Colección: productos

```javascript
db.createCollection('productos');

// Índices
db.productos.createIndex({ nombre: 1 });
db.productos.createIndex({ tipo: 1 });
db.productos.createIndex({ fechaVencimiento: 1 });
db.productos.createIndex({ stock: 1 });

// Documento de ejemplo
db.productos.insertOne({
  nombre: "Amoxicilina 500mg",
  descripcion: "Antibiótico de amplio espectro",
  unidad: "unidad",
  tipo: "medicamento",
  lote: "LOT-2024-A123",
  fechaVencimiento: new Date("2026-12-31"),
  stock: 150,
  stockMinimo: 20,
  precioCompra: 2500,
  precioVenta: 4000,
  proveedores: [
    {
      proveedorId: ObjectId("..."),
      proveedorNombre: "Distribuidora MedVet",
      esPrincipal: true
    }
  ],
  movimientosRecientes: [
    {
      movId: new ObjectId(),
      tipo: "entrada",
      cantidad: 50,
      fecha: new Date("2024-10-20"),
      usuarioId: ObjectId("..."),
      usuarioNombre: "Admin Usuario",
      motivo: "Compra a proveedor"
    }
  ]
});
```

### 7. Colección: proveedores

```javascript
db.createCollection('proveedores');

// Índices
db.proveedores.createIndex({ nombre: 1 });
db.proveedores.createIndex({ nit: 1 }, { unique: true });

// Documento de ejemplo
db.proveedores.insertOne({
  nombre: "Distribuidora MedVet",
  nit: "900123456-7",
  contacto: {
    nombreContacto: "Luis Fernández",
    telefono: "+57 320 789 0123",
    email: "contacto@medvet.com",
    direccion: "Calle 50 #30-40, Medellín"
  },
  activo: true,
  fechaRegistro: new Date()
});
```

### 8. Colección: notificaciones

```javascript
db.createCollection('notificaciones');

// Índices
db.notificaciones.createIndex({ destinatarioId: 1, fechaEnvioPrevisto: -1 });
db.notificaciones.createIndex({ estadoEnvio: 1, fechaEnvioPrevisto: 1 });
db.notificaciones.createIndex({ tipo: 1 });

// Documento de ejemplo
db.notificaciones.insertOne({
  tipo: "recordatorio_cita",
  mensaje: "Recordatorio: Tiene una cita mañana a las 14:00",
  destinatarioId: ObjectId("..."),
  destinatarioEmail: "maria.garcia@email.com",
  fechaEnvioPrevisto: new Date("2024-10-27T14:00:00Z"),
  estadoEnvio: "pendiente",
  citaId: ObjectId("...")
});
```

---

## 🔍 Consultas de Ejemplo

### Buscar citas de un cliente
```javascript
db.citas.find({ clienteNombre: "María García" })
```

### Buscar mascotas de un propietario
```javascript
db.mascotas.find({ propietarioNombre: "María García" })
```

### Buscar productos con stock bajo
```javascript
db.productos.find({ $expr: { $lt: ["$stock", "$stockMinimo"] } })
```

### Buscar medicamentos próximos a vencer (30 días)
```javascript
const fechaLimite = new Date();
fechaLimite.setDate(fechaLimite.getDate() + 30);
db.productos.find({ 
  tipo: "medicamento", 
  fechaVencimiento: { $lte: fechaLimite } 
})
```

### Obtener historia clínica completa de una mascota
```javascript
db.mascotas.findOne(
  { nombre: "Max" },
  { historiaClinica: 1 }
)
```

### Buscar citas pendientes de un veterinario
```javascript
db.citas.find({
  veterinarioNombre: "Dr. Carlos Rodríguez",
  estado: "CONFIRMADA",
  fechaHora: { $gte: new Date() }
}).sort({ fechaHora: 1 })
```

### Facturas pendientes de pago
```javascript
db.facturas.find({ estado: "EMITIDA" })
```

---

## 📊 Comandos de Verificación

### Ver todas las colecciones
```javascript
show collections
```

### Ver índices de una colección
```javascript
db.usuarios.getIndexes()
db.mascotas.getIndexes()
db.citas.getIndexes()
```

### Contar documentos
```javascript
db.usuarios.countDocuments()
db.mascotas.countDocuments()
db.citas.countDocuments()
```

### Estadísticas de una colección
```javascript
db.mascotas.stats()
```

---

## ✅ Ventajas del Diseño

1. **Rendimiento optimizado**: Historia clínica embebida reduce consultas complejas
2. **Flexibilidad**: Esquema puede evolucionar sin migraciones complejas
3. **Escalabilidad**: Las colecciones pueden distribuirse horizontalmente
4. **Desnormalización estratégica**: Nombres duplicados aceleran consultas comunes
5. **Inmutabilidad**: Facturas y documentos históricos preservados
6. **Trazabilidad**: Todos los cambios quedan registrados con fecha y usuario

---

## 🎓 Justificación por Colección

### usuarios
Se usa una colección unificada con discriminador de tipo para centralizar autenticación y gestión de permisos, evitando duplicación de código y consultas.

### mascotas
La historia clínica se embebe porque siempre se consulta junto con los datos de la mascota, mejorando significativamente el rendimiento.

### citas
Colección independiente porque representa relaciones N:N entre mascotas, clientes y veterinarios. La desnormalización de nombres optimiza las consultas de agenda.

### facturas
Los detalles se embeben porque las facturas son documentos inmutables una vez emitidas, lo que hace innecesario mantenerlos separados.

### productos
Se unifican medicamentos e insumos usando discriminador. Los movimientos recientes se embeben limitados a 10 para consultas rápidas de historial.

### proveedores
Colección separada porque los proveedores son entidades independientes con ciclo de vida propio, usadas por múltiples productos.

### notificaciones
Sistema centralizado que permite gestionar notificaciones de múltiples fuentes (citas, inventario, sistema) con tracking de estado de envío.

---

## 📝 Notas Importantes

- Los ObjectId deben ser reemplazados por IDs reales al insertar documentos relacionados
- Las fechas usan formato ISODate de MongoDB
- Los índices mejoran el rendimiento pero consumen espacio en disco
- La validación de esquema puede hacerse más estricta en producción
- Los movimientos de inventario antiguos pueden archivarse en colección separada
- Las notificaciones antiguas pueden eliminarse después de cierto tiempo

---

**Documento elaborado el:** 25 de Octubre de 2025  
**Proyecto:** Sistema de Gestión Veterinaria - Nuclear  
**Materia:** Bases de Datos 2 - Primer Corte

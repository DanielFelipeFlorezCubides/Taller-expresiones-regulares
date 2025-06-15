
# 🛒 Salud y Vida - Gestión de Tienda Natural

## Descripción del Proyecto

**Salud y Vida** es un sistema de gestión para una tienda online de productos naturales, enfocada en suplementos, vitaminas y productos herbales. Este sistema permite registrar la configuración de la tienda, gestionar inventario y realizar el seguimiento de pedidos.

Este proyecto simula un entorno realista en el que se pueden realizar consultas complejas a través de expresiones regulares, útiles para mejorar la búsqueda, detectar patrones, y validar datos de forma más eficiente.

---

## 📦 Estructura de la Base de Datos

La base de datos está conformada por **3 colecciones principales**:

- `configuracion`: Configuración general de la tienda, redes, métodos de pago, envíos, promociones, etc.
- `inventario`: Registro detallado de productos disponibles, lotes, proveedores, movimientos, etc.
- `pedidos`: Información completa de los pedidos, incluyendo productos, pagos, envíos y promociones aplicadas.

---

## 🛠️ Creación de la Base de Datos en MongoDB

1. Abre tu terminal y conéctate a tu instancia de MongoDB:
   ```bash
   mongo
   ```

2. Crea la base de datos:
   ```js
   use salud_y_vida
   ```

3. Importa cada archivo `.json` con el siguiente comando (reemplaza la ruta si es necesario):

   ```bash
   mongoimport --db salud_y_vida --collection configuracion --file configuracion.json --jsonArray
   mongoimport --db salud_y_vida --collection inventario --file inventario.json --jsonArray
   mongoimport --db salud_y_vida --collection pedidos --file pedidos.json --jsonArray
   mongoimport --db salud_y_vida --collection productos --file productos.json --jsonArray
   mongoimport --db salud_y_vida --collection usuarios --file usuarios.json --jsonArray
   ```

---

## 📂 Archivos Incluidos

- `configuracion.json` → Colección: `configuracion`
- `inventario.json` → Colección: `inventario`
- `pedidos.json` → Colección: `pedidos`
- `productos.json` → Colección: `productos`
- `usuarios.json` → Colección: `usuarios`

---

## 🔍 Consultas con Expresiones Regulares (25)

> A continuación, se presentan 25 consultas prácticas utilizando expresiones regulares. Cada una incluye su utilidad dentro del sistema.

### Configuración

**1. Buscar métodos de envío que contienen la palabra "gratis"**
```js
db.configuracion.find({ "envio.metodos.nombre": { $regex: "gratis", $options: "i" } })
```
> Útil para mostrar al cliente las opciones sin costo.

**2. Buscar promociones activas con código que empieza por "VER"**
```js
db.configuracion.find({ "promociones.codigo": { $regex: "^VER" } })
```
> Ayuda a encontrar promociones por temporada como "VERANO2023".

**3. Buscar redes sociales que incluyan "instagram"**
```js
db.configuracion.find({ "redes_sociales.instagram": { $regex: "instagram" } })
```
> Verifica si se tiene cuenta en Instagram.

**4. Buscar categorías que contienen la palabra "suplementos"**
```js
db.configuracion.find({ "categorias_principales.nombre": { $regex: "suplementos", $options: "i" } })
```
> Para filtrar y mostrar solo esa categoría.

**5. Buscar promociones con descripción que incluya "envío"**
```js
db.configuracion.find({ "promociones.descripcion": { $regex: "env[ií]o", $options: "i" } })
```
> Útil para destacar beneficios logísticos.

---

### Inventario

**6. Buscar productos con nombre que inicie con "Omega"**
```js
db.inventario.find({ "nombre_producto": { $regex: "^Omega" } })
```
> Implementación de autocompletado de búsqueda.

**7. Buscar productos cuya ubicación contenga "Estante A"**
```js
db.inventario.find({ "ubicacion": { $regex: "Estante A" } })
```
> Control de almacenamiento físico.

**8. Buscar lotes con código que termine en "001"**
```js
db.inventario.find({ "lotes.codigo": { $regex: "001$" } })
```
> Detectar lotes iniciales o prioritarios.

**9. Buscar proveedores con correo que contiene "labnaturales"**
```js
db.inventario.find({ "proveedor.contacto": { $regex: "labnaturales" } })
```
> Filtro rápido para pedidos al proveedor habitual.

**10. Buscar notas de movimientos que contengan "venta"**
```js
db.inventario.find({ "movimientos.nota": { $regex: "venta", $options: "i" } })
```
> Útil para auditorías y trazabilidad.

---

### Pedidos

**11. Buscar usuarios cuyo correo termina en "@ejemplo.com"**
```js
db.pedidos.find({ "usuario_info.email": { $regex: "@ejemplo\.com$" } })
```
> Filtrado de clientes corporativos o internos.

**12. Buscar pedidos con estado "entregado"**
```js
db.pedidos.find({ "estado": { $regex: "^entregado$" } })
```
> Útil para generar estadísticas de entregas.

**13. Buscar métodos de pago que incluyan "tarj"**
```js
db.pedidos.find({ "pago.metodo": { $regex: "tarj", $options: "i" } })
```
> Análisis de tendencias en formas de pago.

**14. Buscar productos en pedidos con SKU que contiene "MAG"**
```js
db.pedidos.find({ "productos.sku": { $regex: "MAG" } })
```
> Control de pedidos que incluyen magnesio.

**15. Buscar pedidos cuya nota contenga la palabra "portero"**
```js
db.pedidos.find({ "notas": { $regex: "portero", $options: "i" } })
```
> Verifica pedidos con instrucciones especiales.

**16. Buscar nombre de cliente que comienza con "Juan"**
```js
db.pedidos.find({ "usuario_info.nombre": { $regex: "^Juan" } })
```
> Búsqueda directa de cliente.

**17. Buscar ciudad de envío que contiene "Ciudad"**
```js
db.pedidos.find({ "direccion_envio.ciudad": { $regex: "Ciudad", $options: "i" } })
```
> Filtro geográfico para logística.

**18. Buscar pedidos con número que comience en "ORD-"**
```js
db.pedidos.find({ "numero_pedido": { $regex: "^ORD-" } })
```
> Verificación de formatos correctos de pedidos.

**19. Buscar pedidos con código de promoción que contenga "BIEN"**
```js
db.pedidos.find({ "promocion.codigo": { $regex: "BIEN", $options: "i" } })
```
> Analizar rendimiento de códigos de bienvenida.

**20. Buscar proveedores de pago que contengan "Visa"**
```js
db.pedidos.find({ "pago.proveedor": { $regex: "Visa" } })
```
> Revisión de transacciones por proveedor.

**21. Buscar historial de estados que incluya "procesando"**
```js
db.pedidos.find({ "historial_estados.estado": { $regex: "procesando", $options: "i" } })
```
> Seguimiento de pedidos en curso.

**22. Buscar productos en pedidos con nombre que contenga "Vitamina"**
```js
db.pedidos.find({ "productos.nombre": { $regex: "Vitamina", $options: "i" } })
```
> Para detectar qué vitaminas son más populares.

**23. Buscar pedidos con servicio de envío "DHL"**
```js
db.pedidos.find({ "envio.seguimiento.servicio": { $regex: "DHL", $options: "i" } })
```
> Ver seguimiento logístico por proveedor.

**24. Buscar pedidos donde la nota esté vacía**
```js
db.pedidos.find({ "notas": { $regex: "^$" } })
```
> Verificar si se están omitiendo instrucciones.

**25. Buscar dirección de envío con código postal que comience por "123"**
```js
db.pedidos.find({ "direccion_envio.codigo_postal": { $regex: "^123" } })
```
> Segmentación geográfica para campañas.

# Consultas con Expresiones Regulares - Colecciones productos y usuarios

## Búsquedas y Autocompletado

### Consulta 1: Autocompletar productos por nombre
```js
db.productos.find({ "nombre": { "$regex": "^Vita", "$options": "i" } })
```
**Caso de uso:** Barra de búsqueda con autocompletado para sugerir productos cuando el usuario escribe "vita", mostrando "Vitamina C", "Vitamina D", etc.

### Consulta 2: Buscar productos naturales
```js
db.productos.find({ "nombre": { "$regex": "Natural", "$options": "i" } })
```
**Caso de uso:** Filtro en la página de categorías para mostrar solo productos 100% naturales.

### Consulta 3: Productos para sistema inmune
```js
db.productos.find({ "descripcion": { "$regex": "sistema inmune", "$options": "i" } })
```
**Caso de uso:** Página especial de "Productos para Defensas" durante temporada de gripe.

## Análisis de Usuarios

### Consulta 4: Usuarios con Gmail
```js
db.usuarios.find({ "email": { "$regex": "@gmail\\.com$", "$options": "i" } })
```
**Caso de uso:** Estadísticas de marketing para personalizar campañas según proveedor de email.

### Consulta 5: Usuarios mexicanos
```js
db.usuarios.find({ "telefono": { "$regex": "^\\+52", "$options": "i" } })
```
**Caso de uso:** Segmentación por país para promociones específicas y cálculo de envíos.

### Consulta 6: Análisis de género por nombres
```js
db.usuarios.find({ "nombre": { "$regex": "a$", "$options": "i" } })
```
**Caso de uso:** Estadísticas demográficas para personalización de marketing.

## Gestión de Inventario

### Consulta 7: Productos de vitaminas por SKU
```js
db.productos.find({ "sku": { "$regex": "VIT", "$options": "i" } })
```
**Caso de uso:** Reportes de inventario específicos de vitaminas para descuentos masivos.

### Consulta 8: Productos con extractos
```js
db.productos.find({ "especificaciones.ingredientes": { "$regex": "extracto", "$options": "i" } })
```
**Caso de uso:** Crear sección de "Productos con Extractos Herbales".

### Consulta 9: Productos Omega
```js
db.productos.find({ "etiquetas": { "$regex": "omega", "$options": "i" } })
```
**Caso de uso:** Página de categoría específica de ácidos grasos esenciales.

## Control de Calidad

### Consulta 10: Validar códigos postales
```js
db.usuarios.find({ "direcciones.codigo_postal": { "$regex": "^\\d{5}$" } })
```
**Caso de uso:** Validar formatos de códigos postales colombianos y mexicanos para mejorar entregas.

### Consulta 11: Productos con advertencias de embarazo
```js
db.productos.find({ "especificaciones.contraindicaciones": { "$regex": "embarazo", "$options": "i" } })
```
**Caso de uso:** Filtrar productos seguros para usuarias embarazadas.

### Consulta 12: Verificar formato de slugs
```js
db.productos.find({ "slug": { "$regex": "-" } })
```
**Caso de uso:** Verificar que todos los slugs siguen formato SEO con guiones.

## Análisis de Ventas

### Consulta 13: Pedidos del año 2023
```js
db.pedidos.find({ "numero_pedido": { "$regex": "2023", "$options": "i" } })
```
**Caso de uso:** Reportes anuales y estadísticas de ventas por año.

### Consulta 14: Productos con precios psicológicos
```js
db.productos.find({ "precio": { "$regex": "\\.99$" } })
```
**Caso de uso:** Análisis de estrategias de precios terminados en .99.

### Consulta 15: Usuarios con productos premium en carrito
```js
db.usuarios.find({ "carrito.productos.nombre": { "$regex": "Premium", "$options": "i" } })
```
**Caso de uso:** Identificar usuarios interesados en gama alta para cross-selling.

## Atención al Cliente

### Consulta 16: Pedidos urgentes
```js
db.pedidos.find({ "notas": { "$regex": "urgente", "$options": "i" } })
```
**Caso de uso:** Priorizar pedidos marcados como urgentes en el proceso de envío.

### Consulta 17: Reseñas positivas
```js
db.productos.find({ "reseñas.comentario": { "$regex": "recomiendo", "$options": "i" } })
```
**Caso de uso:** Identificar reseñas positivas para testimonios destacados.

### Consulta 18: Direcciones en avenidas principales
```js
db.usuarios.find({ "direcciones.calle": { "$regex": "(Av\\.|Avenida)", "$options": "i" } })
```
**Caso de uso:** Optimizar rutas de reparto en zonas urbanas principales.

## Mantenimiento de Datos

### Consulta 19: Usuarios registrados por mes
```js
db.usuarios.find({ "fecha_registro": { "$regex": "2023-01" } })
```
**Caso de uso:** Análisis de crecimiento mensual y campañas de retención.

### Consulta 20: Productos inactivos
```js
db.productos.find({ "estado": { "$regex": "^(?!activo$).*", "$options": "i" } })
```
**Caso de uso:** Encontrar productos que necesitan revisión o reactivación.

### Consulta 21: Emails con números
```js
db.usuarios.find({ "email": { "$regex": "\\d", "$options": "i" } })
```
**Caso de uso:** Detectar patrones de registro sospechosos o cuentas automatizadas.

### Consulta 22: Productos con nombres simples
```js
db.productos.find({ "nombre": { "$regex": "^\\w+$" } })
```
**Caso de uso:** Identificar productos que necesitan descripciones más detalladas.

### Consulta 23: Direcciones con formato Bis
```js
db.usuarios.find({ "direcciones.calle": { "$regex": "(B\\.|Bis)", "$options": "i" } })
```
**Caso de uso:** Estandarizar formatos de direcciones para mejor precisión.

### Consulta 24: Usuarios con apellidos específicos
```js
db.usuarios.find({ "apellido": { "$regex": "^L", "$options": "i" } })
```
**Caso de uso:** Campañas de marketing personalizadas por inicial del apellido.

### Consulta 25: Validación de productos activos
```js
db.productos.find({ 
  "estado": "activo",
  "nombre": { "$not": { "$regex": "^\\s*$" } }
})
```
**Caso de uso:** Verificar que todos los productos activos tienen nombres válidos.

## Notas de Implementación

- Usar `$options: "i"` para búsquedas insensibles a mayúsculas/minúsculas
- Escapar caracteres especiales con `\\` en las expresiones regulares
- Combinar regex con otros filtros para consultas más específicas
- Considerar índices de texto para búsquedas más complejas
- Usar `limit()` en autocompletado para mejorar performance


---

## ✅ Estado del Proyecto

- [x] Base de datos creada
- [x] Archivos `.json` importables incluidos
- [x] 25 consultas con expresiones regulares prácticas
- [x] Repositorio preparado para entrega

---

## ✍️ Autores
- Daniel Felipe Florez Cubides
- Mateo Paternina Mercado

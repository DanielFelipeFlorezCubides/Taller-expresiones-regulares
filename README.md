
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
   ```

---

## 📂 Archivos Incluidos

- `configuracion.json` → Colección: `configuracion`
- `inventario.json` → Colección: `inventario`
- `pedidos.json` → Colección: `pedidos`

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

---

## ✅ Estado del Proyecto

- [x] Base de datos creada
- [x] Archivos `.json` importables incluidos
- [x] 25 consultas con expresiones regulares prácticas
- [x] Repositorio preparado para entrega

---

## 📅 Fecha de Entrega

**15 de Junio de 2025, 11:59 p.m.**

# Amoly

**Amoly** es una app de gestión y punto de venta (POS) pensada para **kioscos, despensas y comercios chicos**. Permite llevar el control de productos, stock, ventas y empleados desde el celular, con un asistente (chatbot) para hacer consultas rápidas sin tener que navegar por la app.

Es **multi-negocio (multi-tenant)**: muchos comercios usan la misma app, pero cada uno ve únicamente sus propios datos.

---

## ✨ Funciones principales

### Para el dueño
- Crear y administrar uno o varios negocios.
- Dar de alta a los empleados (cada uno con su propio usuario y contraseña).
- Ver el panel del negocio: ventas, ingresos, ganancias y reportes.
- Ver las ventas de todos los empleados.
- Gestionar productos, precios y stock.
- Configurar el negocio.

### Para el empleado
- Registrar ventas.
- Ver el catálogo de productos y el stock disponible.
- Agregar, editar y borrar productos.
- Ver **su propio total de ventas del día**.
- **No** puede ver ganancias, ingresos ni reportes del negocio, ni las ventas de otros empleados, ni gestionar empleados o la configuración.

> Una misma persona puede trabajar en varios negocios, y un dueño puede tener más de un negocio.

### Chatbot integrado
Un asistente dentro de la app (widget de chat) que responde consultas rápidas en lenguaje natural, por ejemplo:
- "¿Cuántas gaseosas de 2 L quedan?"
- "¿Qué productos están por debajo del stock mínimo?"
- "¿Cuánto vendí hoy?"

El chatbot respeta los mismos permisos que la app: un empleado solo puede consultar lo que tiene permitido ver.

### Alertas de stock
Cada producto tiene un **stock mínimo**; la app permite identificar los productos que hay que reponer.

---

## 🧱 Tecnologías

| Parte | Tecnología |
|---|---|
| Frontend (app móvil) | [FlutterFlow](https://flutterflow.io) |
| Base de datos y autenticación | [Supabase](https://supabase.com) (PostgreSQL + Supabase Auth) |
| API backend | Node.js + Express |
| Chatbot | API de Claude (Anthropic) |
| Plataformas | Android (Google Play) e iOS (App Store) |

---

## 🗄️ Modelo de datos

| Tabla | Descripción |
|---|---|
| `businesses` | Negocios registrados. Cada uno tiene un dueño (`owner_id`). |
| `employees` | Empleados de cada negocio, vinculados a su usuario (`user_id`). |
| `products` | Productos con precio, stock y stock mínimo (`min_stock`). |
| `sales` | Ventas registradas (quién vendió, cuándo, total). |
| `sale_items` | Detalle de cada venta (productos y cantidades). |

## 🔒 Seguridad

- **Row Level Security (RLS)** activado en todas las tablas.
- Cada negocio solo accede a sus propios datos (aislamiento multi-tenant).
- Permisos diferenciados por rol (**Dueño** / **Empleado**) aplicados directamente en la base de datos.
- Al iniciar sesión, la app detecta automáticamente el rol del usuario y lo dirige a la pantalla correspondiente.

---

## 📁 Repositorios relacionados

- [`amoly-api`](https://github.com/umiiluni/amoly-api) — backend del chatbot.

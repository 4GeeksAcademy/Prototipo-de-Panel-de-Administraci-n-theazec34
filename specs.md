# SPECS.md — Panel de Administración AgentHub

## Descripción del producto

AgentHub es una plataforma de gestión de agentes de IA que permite a empresas contratar, configurar y monitorizar agentes inteligentes especializados. El panel de administración está orientado a administradores de la plataforma, que necesitan una interfaz centralizada para gestionar usuarios, agentes, skills, contratos y errores del sistema.

## Stack y restricciones

- HTML semántico
- Tailwind CSS por CDN (v4: `https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4`)
- Si se necesita CSS adicional, debe ir exclusivamente en `styles.css` (importado con `<link>`) — nunca dentro de un bloque `<style>` en el HTML
- JavaScript vanilla (sin frameworks)
- Datos hardcodeados (sin backend)
- Sin CSS inline ni estilos en atributo `style=""`

## Secciones y requisitos

### Dashboard

1. Cuatro tarjetas métricas con los KPIs principales: Total de usuarios, Total de agentes, Skills activas y Contratos pendientes. Cada tarjeta muestra el nombre de la métrica y su valor numérico destacado.
2. Un área reservada para un gráfico de actividad (placeholder visual con borde discontinuo), preparada para conectar una librería de gráficos en el futuro.
3. Layout responsive en grid: 1 columna en móvil, 2 en tablet, 4 en escritorio.

### Gestión de usuarios

1. Tabla con columnas: Nombre, Email, Rol, Estado (badge de color) y Acciones. Incluye al menos 2 usuarios de ejemplo con datos distintos (uno activo, uno inactivo).
2. Botón "Agregar Usuario" en la cabecera de la sección. Al hacer clic abre un modal con formulario de creación (campos: Nombre, Email, Rol).
3. Cada fila tiene un menú desplegable de tres puntos (⋮) con opciones "Editar" (abre modal de edición) y "Eliminar". El modal de edición pre-rellena los campos con los datos del usuario.

### Gestión de agentes

1. Lista de tarjetas, una por agente, con nombre, descripción corta y menú de acciones (⋮) con opciones "Configurar" y "Eliminar". Al menos 2 agentes de ejemplo.
2. Cada tarjeta tiene un botón "Ver Skills" que despliega/colapsa una lista de las skills asignadas al agente (comportamiento accordion/colapsable con transición suave).
3. "Configurar" abre un modal con formulario de edición del agente (campos: Nombre, Descripción).

### Skills

1. Grid de tarjetas, 1 columna en móvil, 2 en tablet, 3 en escritorio. Cada tarjeta muestra nombre y descripción de la skill. Al menos 3 skills de ejemplo.
2. Cada tarjeta tiene un menú desplegable (⋮) con opciones "Editar" y "Eliminar".
3. El nombre y la descripción deben ser suficientemente descriptivos para representar capacidades reales de un agente IA (ej. "Redacción de emails", "Análisis de datos", "Soporte al cliente").

### Contrataciones

1. Tabla con columnas: ID, Cliente, Fecha, Estado (badge de color: Pendiente en amarillo, Completado en azul) y Acciones. Al menos 2 contratos de ejemplo.
2. Botón "Ver Detalle" en cada fila que abre un modal con la información completa del contrato (ID, Cliente, Fecha, Estado, Descripción).
3. El modal de detalle es de solo lectura; incluye un botón "Cerrar" para descartarlo.

### Log de errores

1. Tabla con columnas: Fecha/hora, Tipo (ej. Database, API, Auth), Mensaje del error, Severidad (badge: Error en rojo, Advertencia en naranja) y Acciones.
2. Botón "Ver Detalle" que abre un modal con la información completa del error incluyendo el Stack Trace.
3. Al menos 2 entradas de log de ejemplo con distintas severidades.

## Inventario de componentes reutilizables

- **Sidebar**: navegación lateral fija con botones de sección; el botón activo se resalta en azul.
- **Topbar**: barra superior con título de la app y botón de toggle de tema claro/oscuro.
- **Tarjetas métricas**: contenedor blanco/dark con título y valor numérico grande.
- **Tabla**: estructura semántica `<table>` con cabecera, filas con separadores y soporte dark mode.
- **Badge**: pastilla de color con texto para representar estados. Variantes: active (verde), inactive (rojo), pending (amarillo), completed (azul), error (rojo), warning (naranja).
- **Dropdown (menú ⋮)**: menú contextual posicionado absolutamente, se abre al pulsar el botón de tres puntos y se cierra al hacer clic fuera.
- **Modal**: capa con overlay oscuro centrada en pantalla, se cierra al pulsar el botón de cierre o el fondo.
- **Colapsable de skills**: sección expandible/contraíble con transición CSS, usada dentro de las tarjetas de agentes.
- **Toggle de tema**: botón en la topbar que alterna entre modo claro y oscuro añadiendo/quitando la clase `dark` en el `<html>` y persiste la preferencia en `localStorage`.

## Criterios de aceptación

1. Todas las secciones son accesibles desde el sidebar sin recargar la página (navegación SPA con show/hide de secciones).
2. El modo oscuro funciona correctamente en todos los componentes y persiste al recargar la página.
3. Todos los modales y dropdowns abren y cierran sin errores; hacer clic fuera del modal o del dropdown los cierra automáticamente.
4. El diseño es responsive: se adapta correctamente a pantallas de móvil, tablet y escritorio.
5. No existe ningún CSS en etiquetas `<style>` dentro del HTML ni en atributos `style=""`. Todo el CSS adicional va en `styles.css`.

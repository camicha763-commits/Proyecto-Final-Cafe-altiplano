# Café Altiplano - Proyecto Final de Desarrollo Web

Sitio web multipágina desarrollado con **HTML5 y CSS3** para la cafetería de especialidad **Café Altiplano**. El proyecto está estructurado con enfoque *mobile-first*, maquetado con **CSS Grid** y diseñado bajo principios de semántica, accesibilidad y coherencia visual en tonos café, crema, beige y verde oliva.

---

## 1. Mapa del sitio

El sitio consta de cuatro páginas enlazadas mediante una barra de navegación fija y coherente:

* **Inicio (`index.html`):**
  * Cabecera con logotipo textual y menú principal con indicador de página activa (`aria-current="page"`).
  * Portada principal con imagen de fondo destacada, presentación y botones de llamada a la acción.
  * Sección "Nuestra propuesta" con descripción y lista desordenada (`<ul>`).
  * Horario general presentado en una lista de definición (`<dl>`, `<dt>`, `<dd>`) dentro de un bloque informativo.
  * Sección "Productos destacados" con galería de tarjetas (`<article>`, `<figure>`, `<img>`, `<figcaption>`).
  * Pie de página unificado con derechos de autor.

* **Carta (`carta.html`):**
  * Portada informativa.
  * Menú de anclas internas para navegación rápida a cada sección (`#calientes`, `#frias`, `#acompanamientos`).
  * Sección "Bebidas calientes": galería visual y tabla estructurada con precios (`<caption>`, `<thead>`, `<tbody>`, `<th>`, `<td>`).
  * Sección "Bebidas frías": tarjeta descriptiva y tabla con opciones y precios.
  * Sección "Acompañamientos": repostería artesanal con imágenes y tabla de porciones.
  * Sección filosófica con cita textual utilizando `<blockquote class="cita">` y `<cite>`.

* **Sedes (`sedes.html`):**
  * Portada descriptiva.
  * Galería con las tres sedes físicas (Centro, Norte y Sur).
  * Tarjetas individuales con fotografías de fachadas e interiores, direcciones, horarios, teléfonos y correos ficticios, enlaces a mapas externos y enlace directo a reservas.

* **Reservas (`reservas.html`):**
  * Portada del servicio.
  * Sección explicativa "Cómo funciona" mediante una lista ordenada (`<ol>`).
  * Formulario accesible de reserva estructurado con `<fieldset>` y `<legend>`, etiquetas `<label>` vinculadas a sus respectivos controles (`input text`, `email`, `tel`, `date`, `time`, `number`, `select`, `radio`, `textarea` y `checkbox`).
  * Todos los campos principales cuentan con atributo `required`.
  * Nota informativa sobre la política de tolerancia en la reserva.

---

## 2. Tabla de comportamiento responsive

Comportamiento del maquetado en los tres anchos de referencia:

| Elemento / Sección | Móvil (500 px) | Tableta (800 px) | Computador (1200 px) |
| :--- | :--- | :--- | :--- |
| **Cuadrícula general (`body`)** | 1 columna (`1fr`), flujo vertical apilado | 2 columnas (`repeat(2, 1fr)`) | 3 columnas (`repeat(3, 1fr)`) |
| **Cabecera (`header`)** | Logotipo centrado arriba y menú en cuadrícula | 2 columnas: logotipo a la izquierda, menú a la derecha | 2 columnas alineadas con ancho máximo de 70rem centrado |
| **Portadas y pie de página** | Ancho completo (`grid-column: 1 / -1`) | Ancho completo (`grid-column: 1 / -1`) | Ancho completo (`grid-column: 1 / -1`) |
| **Galerías de tarjetas (`.galeria`)** | 1 columna por tarjeta (se acomoda con `minmax(14rem, 1fr)`) | 2 columnas automáticas | 3 columnas automáticas según el espacio disponible |
| **Bloques anchos (`.bloque--ancho`)** | 1 columna (ancho disponible) | Ocupa 2 columnas (`span 2`) | Ocupa 2 columnas (`span 2`), dejando 1 columna para aside/notas |
| **Tablas de precios** | Desplazamiento horizontal seguro mediante `.tabla-contenedor` | Tabla expandida al 100% del contenedor sin desplazamiento | Tabla integrada con lectura cómoda y filas alternas |
| **Formulario de reserva** | Campos apilados verticalmente a ancho completo | Campos distribuidos en bloque ancho de 2 columnas | Centrado en bloque ancho con notas complementarias al lado |

---

## 3. Justificación de cinco unidades CSS utilizadas

1. **`rem` (Root EM):**
   Utilizada para el tamaño de las fuentes (`font-size: 1.75rem`, `1.25rem`, etc.) y los espaciados principales (`padding`, `margin`, `gap`). Permite que el diseño respete las preferencias de accesibilidad configuradas por el usuario en su navegador.
2. **`px` (Píxeles absolutos):**
   Reservada estrictamente para bordes finos (`1px solid var(--color-borde)` y `0.25rem` / `3px` en líneas de resalte). Garantiza que las líneas divisorias y bordes mantengan nitidez independientemente de la resolución de pantalla.
3. **`ch` (Ancho del carácter '0'):**
   Aplicada en los párrafos (`max-width: 65ch;`). Asegura una medida de lectura óptima recomendada en diseño editorial web (entre 50 y 75 caracteres por línea), evitando líneas excesivamente largas en monitores grandes.
4. **`%` (Porcentaje):**
   Utilizada en elementos fluidos como imágenes (`max-width: 100%`) y tablas (`width: 100%`), permitiendo que el contenido se adapte elásticamente al tamaño del contenedor padre.
5. **`vh` (Viewport Height):**
   Empleada en las portadas (`min-height: 40vh` para páginas internas y `min-height: 85vh` para la portada principal de inicio). Garantiza una presencia visual proporcionada con relación al alto visible de la ventana del dispositivo.

---

## 4. Mobile First y puntos de ruptura

La metodología **Mobile First** establece que los estilos base del sitio web se definen pensando en la experiencia en dispositivos móviles (pantallas pequeñas), donde la interfaz debe ser simple, vertical y directa.

A partir de esa base, se utilizan consultas de medios (*media queries*) exclusivamente con `min-width` para añadir columnas y complejidad visual de manera progresiva a medida que la pantalla crece:

* **Base (< 600 px):** Maquetación a 1 sola columna. Menús y tarjetas apiladas, sin elementos flotantes ni columnas complejas.
* **Punto de ruptura 1 (`@media (min-width: 600px)`):** Se activa para tabletas en adelante. El cuerpo pasa a 2 columnas de igual ancho (`repeat(2, 1fr)`), la cabecera distribuye el logotipo y el menú horizontalmente, y los bloques marcados como `.bloque--ancho` se extienden a lo largo de las dos columnas.
* **Punto de ruptura 2 (`@media (min-width: 900px)`):** Se activa para computadores de escritorio. La cuadrícula del `body` pasa a 3 columnas (`repeat(3, 1fr)`), permitiendo una composición más rica donde conviven secciones anchas (2 columnas) con notas laterales (1 columna), enmarcadas dentro de un contenedor centrado de hasta `70rem`.

---

## 5. Dificultad encontrada y solución

* **Dificultad:** Presentar tablas de precios con múltiples columnas y galerías fotográficas en pantallas de teléfono móvil sin provocar desplazamiento horizontal indeseado en la página (`overflow-x`), cumpliendo a la vez la restricción estricta de **no utilizar Flexbox**.
* **Solución:**
  1. Para las tablas, se envolvió cada una dentro de un contenedor semántico `<div class="tabla-contenedor">` con la propiedad CSS `overflow-x: auto;`. De esta forma, si la pantalla es muy estrecha (500 px o menos), la tabla se puede deslizar localmente con el dedo o ratón sin deformar ni ensanchar la página principal.
  2. Para las galerías, se utilizó CSS Grid con la función `repeat(auto-fit, minmax(14rem, 1fr))`, lo que permite que las tarjetas salten de fila automáticamente cuando no caben, sin necesidad de definir media queries manuales para cada tamaño.

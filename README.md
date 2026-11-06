# Ruta Opita

Landing page académica para presentar ideas de viaje por el Huila. Construida con HTML, Tailwind CSS 4 mediante Play CDN y JavaScript sin librerías adicionales.

**Sitio publicado:** <https://luislaureanobe-stack.github.io/ruta-opita/>
**Repositorio:** <https://github.com/luislaureanobe-stack/ruta-opita>
**Autor:** Luis Armando Laureano Betanconurth
**Asignatura:** Seminario en Gestión de Software Ágil Asistido por IA · Módulo 3
**Docente:** Camilo Morales Vargas

---

## Cómo abrir

1. Descarga o clona el repositorio.
2. Abre `index.html` en un navegador moderno.
3. Se necesita conexión a internet para cargar Tailwind Play CDN y Google Fonts.

---

## Prompt maestro

Este es el prompt que se usó para generar la primera versión del sitio. Tiene las cinco partes que pide la guía.

> **Rol:** Actúa como desarrollador frontend senior especializado en Tailwind CSS 4, diseño responsive y accesibilidad web.
>
> **Contexto:** Voy a crear la landing page de "Ruta Opita", un proyecto académico que presenta ideas de viaje por el departamento del Huila (Colombia): el Desierto de la Tatacoa, el patrimonio arqueológico de San Agustín, los termales y las rutas del occidente. El público son viajeros jóvenes y familias de 20 a 45 años que buscan información clara antes de organizar un recorrido de dos o tres días. El objetivo del sitio es dar a conocer cuatro rutas, contar qué hace particular a la región y recibir solicitudes de información por medio de un formulario.
>
> **Tareas:** Construye un único archivo `index.html` con estas secciones, en este orden:
> 1. Navbar fija con el logo en texto, enlaces a cada sección y un botón "Planea tu viaje"; en móvil los enlaces se convierten en un menú hamburguesa que se abre y se cierra con JavaScript.
> 2. Hero con titular, subtítulo, imagen de fondo con capa oscura y dos botones.
> 3. Sección de rutas en tarjetas: una columna en celular, dos en tablet y cuatro en computador; cada tarjeta con imagen, nombre, descripción breve y una etiqueta de duración.
> 4. Sección "Nuestra tierra" con texto a un lado e imagen al otro.
> 5. Preguntas frecuentes en acordeón, con mínimo tres preguntas, que se abran y se cierren con JavaScript.
> 6. Formulario de contacto con nombre, correo, selector de experiencia y mensaje; validación con JavaScript de los campos obligatorios y del formato del correo, mensaje de error debajo de cada campo y aviso de confirmación que desaparece a los cuatro segundos.
> 7. Pie de página con datos del proyecto y un enlace para volver arriba.
> Agrega un botón para alternar entre modo claro y oscuro, y guarda la preferencia en el navegador.
>
> **Restricciones:**
> - Usa solo HTML, Tailwind CSS 4 por Play CDN (`https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4`) y JavaScript puro. Sin frameworks ni librerías.
> - Define la paleta con `@theme` dentro de una etiqueta `<style type="text/tailwindcss">`. Regla 60‑30‑10: fondo crema `#F6F3E9` (60 %), verde bosque `#234537` (30 %) y dorado `#D5A84A` (10 %); más verde de éxito `#166534`, rojo de error `#B42318` y ámbar de advertencia `#8A4B00`.
> - Máximo dos fuentes de Google Fonts: Manrope para títulos y DM Sans para el texto.
> - Diseña mobile-first y usa los prefijos `sm:`, `md:` y `lg:`.
> - Cumple accesibilidad: texto alternativo descriptivo en las imágenes, etiquetas asociadas a cada campo, contraste mínimo de 4,5:1 en el texto y foco visible en todos los elementos interactivos.
> - El modo oscuro se activa con una clase `dark` en `<html>`; declara la variante con `@custom-variant dark (&:where(.dark, .dark *))`.
>
> **Formato de salida:** entrega un solo archivo `index.html`, con el JavaScript al final del `body`, el código indentado, comentarios en español que separen cada sección y nombres de clase semánticos del tema (`bg-brand-cream`, `text-brand-forest`). Al final, explica en una lista corta qué partes conviene personalizar y cómo abrir el archivo.

---

## Bitácora de prompts e iteraciones

Cada fila registra un problema observado al abrir el sitio en el navegador, el prompt de ajuste que se envió y lo que pasó.

| # | Prompt de ajuste enviado | Problema que buscaba resolver | Resultado obtenido | ¿Funcionó? |
|---|---|---|---|---|
| 1 | «Estoy usando Tailwind 4 por Play CDN, no existe `tailwind.config.js`. Reescribe la configuración del tema usando `@theme` y declara el modo oscuro con `@custom-variant`, no con `darkMode: 'class'`.» | La primera respuesta traía sintaxis de la versión 3: directivas `@tailwind base/components/utilities` y un objeto `tailwind.config.js`. En Tailwind 4 no compila. | Devolvió el bloque `<style type="text/tailwindcss">` con `@theme` y `@custom-variant`. Los colores empezaron a generar utilidades (`bg-brand-cream`, `text-brand-forest`). | Sí |
| 2 | «El menú hamburguesa se queda abierto después de tocar un enlace. Ciérralo al elegir un destino y actualiza `aria-expanded` y `aria-label` del botón.» | En móvil, al tocar "Rutas" la página bajaba pero el panel seguía desplegado y tapaba el contenido. | Añadió un `forEach` sobre `.mobile-link` que oculta el panel y reinicia los atributos ARIA. Verificado en el navegador con el modo responsive. | Sí |
| 3 | «En modo oscuro, las opciones del `<select>` se ven con texto negro sobre fondo oscuro. Corrige el contraste solo de la lista desplegable sin cambiar el resto del formulario.» | El campo se veía bien, pero al desplegarlo las opciones eran ilegibles porque el navegador las pinta con el color del sistema. | Propuso estilos para `#interest option` y su variante `.dark`. Se ajustaron a los colores del tema y quedó legible en ambos modos. | Sí |
| 4 | «La validación solo usa el atributo `required` del navegador. Valida el correo con una expresión regular, muestra el mensaje debajo del campo afectado, marca el campo con `aria-invalid` y lleva el foco al primer error.» | Al enviar vacío, el navegador mostraba su burbuja nativa y un campo con error quedaba sin resaltar ni explicar. | Implementó `showError`/`clearError`, la expresión regular del correo y el `focus()` sobre el primer `[aria-invalid="true"]`. Funcionó; se añadió a mano el `aria-describedby` que faltaba. | Sí |
| 5 | «El aviso de confirmación aparece visualmente pero un lector de pantalla no lo anuncia. Hazlo accesible sin cambiar su apariencia.» | El toast se mostraba, pero no era detectable por tecnología de asistencia. | Añadió `role="status"` y `aria-live="polite"`. El cambio fue de una línea y no alteró el diseño. | Sí |

**Lo que la IA hizo mal y hubo que corregir a mano:** usó sintaxis de Tailwind 3 en el primer intento, propuso `focus-visible:outline-brand-gold` (dorado sobre crema, 1,99:1, por debajo del mínimo), dejó el selector de experiencia y el mensaje fuera de la validación, y no incluyó el cierre del menú con la tecla Escape.

---

## Los tres cambios manuales (sin IA)

Se hicieron sobre `index.html` después de la última iteración, y están explicados para el video.

### Cambio 1 — Contraste del anillo de foco

El sitio tenía `focus-visible:outline-brand-gold` en 17 elementos. El dorado `#D5A84A` sobre el fondo crema `#F6F3E9` da **1,99:1**, por debajo del 3:1 que exige WCAG 2.2 para componentes de interfaz: el foco existía pero era casi invisible.

**Antes**

```html
focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-brand-gold
```

**Después**

```html
focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-brand-forest dark:outline-brand-gold
```

Ahora el contorno es verde bosque `#234537` sobre crema (**9,56:1**) y dorado sobre el verde pino del modo oscuro (**6,11:1**). Se corrigieron 16 elementos; el enlace del pie de página conserva el dorado porque su fondo ya es verde pino y ahí sí cumple.

En la misma revisión apareció un segundo problema, que Lighthouse detectó después: la etiqueta «Paisajes que cuentan historias» iba en `text-brand-gold` sobre un panel claro translúcido. El fondo real compuesto es `#2E4E41` y el dorado daba **4,18:1**, por debajo de 4,5:1. Se agregó al tema un dorado claro para texto sobre superficies oscuras:

```css
--color-brand-gold-soft: #E8C87E;   /* 5,69:1 sobre #2E4E41 */
```

### Cambio 2 — El selector de experiencia pasa a ser obligatorio

El formulario validaba solo el nombre y el correo. El `<select>` de experiencia y el mensaje no tenían `required`, ni `aria-describedby`, ni párrafo de error. Se añadieron al HTML:

```html
<label for="interest">¿Qué experiencia te interesa? <span aria-hidden="true">*</span></label>
<select id="interest" name="interest" required aria-describedby="interest-error"> … </select>
<p id="interest-error" class="mt-1 hidden text-sm text-state-error" aria-live="polite"></p>
```

y al JavaScript, la regla y la limpieza del error al cambiar de opción:

```js
if (!interest.value) {
  showError(interest, 'Elige la experiencia que te interesa.');
  isValid = false;
}
```

Con eso quedan tres campos obligatorios y el foco salta al primero que falle.

### Cambio 3 — Cerrar el menú móvil con la tecla Escape

El panel solo se cerraba con el botón o al tocar un enlace. Se añadió un manejador que además devuelve el foco al botón, para no dejar al usuario de teclado perdido:

```js
document.addEventListener('keydown', (event) => {
  if (event.key !== 'Escape') return;
  if (menuButton.getAttribute('aria-expanded') !== 'true') return;
  mobileMenu.classList.add('hidden');
  menuButton.setAttribute('aria-expanded', 'false');
  menuButton.setAttribute('aria-label', 'Abrir menú');
  menuButton.focus();
});
```

---

## Verificación

- **Validador HTML:** revisado en <https://validator.w3.org/nu/>. Reporta **3 errores, todos en el bloque de Tailwind** y ninguno en la estructura del documento: el atributo `type="text/tailwindcss"` no es un valor admitido para `<style>`, y el validador no reconoce las at-rules `@theme` ni `@custom-variant`. Son inevitables al usar el Play CDN y desaparecen si se compila con el CLI: ahí el bloque se convierte en un archivo `.css` normal. El resto del marcado —etiquetas, anidamiento, atributos ARIA— no presenta objeciones.
- **Accesibilidad:** auditoría con Lighthouse 12.8 en Chrome, preset de escritorio. **Puntaje: 100/100**, sin hallazgos automáticos. Evidencia en `docs/lighthouse.png` y el reporte completo en `docs/lighthouse.report.html`.
- **Contraste:** los pares de la paleta se midieron en <https://webaim.org/resources/contrastchecker/>:

| Combinación | Uso | Ratio |
|---|---|---|
| `#1E2A22` sobre `#F6F3E9` | Texto principal | 13,42:1 |
| `#58675E` sobre `#F6F3E9` | Texto secundario | 5,38:1 |
| `#FFFFFF` sobre `#234537` | Texto de botones | 10,62:1 |
| `#F6F3E9` sobre `#173429` | Texto en modo oscuro | 12,13:1 |
| `#D5A84A` sobre `#173429` | Acento en modo oscuro | 6,11:1 |
| `#E8C87E` sobre `#2E4E41` | Etiqueta sobre panel oscuro | 5,69:1 |
| `#B42318` sobre `#F6F3E9` | Error | 5,92:1 |

- **Responsive:** probado a 390 px (celular), 768 px (tablet) y 1280 px (computador).

---

## Secciones y funciones

- Navegación de escritorio y menú hamburguesa para móvil.
- Hero, rutas/destinos, sección sobre turismo responsable, preguntas frecuentes y formulario.
- Tema claro/oscuro persistente en el navegador.
- Acordeón de preguntas con atributos accesibles.
- Validación de nombre, correo y experiencia, con errores junto a cada campo y aviso de confirmación.
- Paleta personalizada en `@theme`; fuentes DM Sans y Manrope.
- Diseño responsive con prefijos `sm:`, `md:` y `lg:`; foco visible, etiquetas y texto alternativo descriptivo.

## Límites de esta versión

- El formulario es demostrativo: valida en el navegador, muestra confirmación y no envía ni almacena datos.
- Las imágenes de destino son bloques ilustrativos en CSS. Antes de publicar, reemplázalos por fotografías propias o con licencia adecuada y conserva la atribución si corresponde.
- Las rutas son contenido promocional de ejemplo; verifica recomendaciones locales y datos operativos antes de presentarlos como información vigente.

## Publicación

Publicado con GitHub Pages desde la rama `main`, carpeta `/ (root)`:

- **Sitio:** <https://luislaureanobe-stack.github.io/ruta-opita/>
- **Repositorio:** <https://github.com/luislaureanobe-stack/ruta-opita>
- Verificado con respuesta HTTP 200 y apertura desde el celular.

## Fuentes de contenido y técnica

- Tailwind Labs. (s. f.). *Play CDN*. https://tailwindcss.com/docs/installation/play-cdn
- Tailwind Labs. (s. f.). *Theme variables*. https://tailwindcss.com/docs/theme
- MDN Web Docs. (s. f.). *CSS: hojas de estilo en cascada*. https://developer.mozilla.org/es/docs/Web/CSS
- W3C. (2023). *Web Content Accessibility Guidelines (WCAG) 2.2*. https://www.w3.org/TR/WCAG22/
- Gobernación del Huila. (s. f.). *Destino turístico y cultural*. https://www.huila.gov.co/publicaciones/5147/destino-turistico-y-cultural/
- Alcaldía de Neiva. (s. f.). *Neiva en turismo*. https://www.alcaldianeiva.gov.co/MiMunicipio/Paginas/Neiva-en-Turismo.aspx
- UNESCO World Heritage Centre. (s. f.). *San Agustín Archaeological Park*. https://whc.unesco.org/en/list/744/

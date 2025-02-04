---
title: How I built this website (v.1.0.2)
date: 2025-02-03
---
Disclaimer:  <10% AI written, >90% AI proofread (uno con el otro jajaja), I jolted down some the main notes of this blog. I didn't allow me some time to re-estructure said notes in a *human™* matter. This one is also in spanish btw.

# Refactorización y Estructuración del Blog

En este post, comparto los cambios recientes que he realizado en la estructura y estilos de mi blog. El objetivo fue mejorar la organización del código, separar responsabilidades y preparar el terreno para futuras actualizaciones.

---

## 1. Añadí una Imagen

Para mejorar la experiencia visual, añadí una imagen relevante en la página de inicio. Esto ayuda a captar la atención de los visitantes y a transmitir mejor la esencia del contenido.

---

## 2. Ajustes en el Footer

Realicé algunos ajustes en el footer para que se vea más coherente con el diseño general del sitio. Estos cambios incluyen mejoras en la alineación, espaciado y tipografía.

---

## 3. Refactorización del Layout Principal

### 3.1. Ajuste del `default layer` de `index`

Modifiqué el `default layer` del archivo `index` para definir un `main` más versátil. Este `main` hace referencia a un partial llamado `homepage/hero.html`.

#### 3.1.1. Creación del Partial `homepage/hero.html`

En este partial, creé un HTML básico con la información que quiero mostrar en la landing page:
- **Hero text**: Un texto destacado que resume la esencia del blog.
- **Dos columnas**: Una estructura de dos columnas para organizar el contenido.
- **Imagen**: Una imagen relevante para acompañar el texto.
- **Redes sociales**: Enlaces a mis perfiles en redes sociales.

#### 3.1.2. Añadir Estilos con SASS

Ahora, resta añadir los estilos a este HTML. Para ello, utilicé SASS para gestionar los estilos de manera más eficiente.

#### 3.1.3. Reestructuración del SASS

Reorganicé el SASS para que todos los estilos se ejecuten desde un solo punto de entrada: `main.css`. Los demás estilos deben ser específicos para cada sección del sitio, siguiendo el principio de **separación de preocupaciones**.

#### 3.1.4. Separación de Módulos CSS

Dividí los diferentes módulos de CSS en archivos separados para facilitar el mantenimiento y la escalabilidad:
- **Home**: Estilos específicos para la página de inicio.
- **Footer**: Estilos generales para el footer.
- **About**: Estilos para la sección "Acerca de mí".
- **Navbar**: Estilos para la barra de navegación.
- **Post**: Estilos para las entradas del blog.

En el futuro, probablemente añadiré más módulos y subcarpetas para organizar mejor los estilos relacionados.

---

## 4. Refactorización de Estilos

Durante el proceso de refactorización, noté que los estilos SCSS que tenía anteriormente se aplicaban a todo el sitio web. Originalmente, estos estilos estaban pensados para visualizar "calmadamente" mis notas contemplativas o posts.

Para solucionar esto, separé los estilos de las notas utilizando **tags** en los layouts y HTML. Esto permite que los estilos generales del sitio web (con un enfoque "medianamente profesional") sean diferentes de los estilos más personales y contemplativos de mis notas.

---

## 5. Estado Actual del Blog

Actualmente, el blog cuenta con:
- **Homepage**: Con sus propios estilos.
- **About Me**: Con estilos diferentes y personalizados.
- **Blogs**: Con estilos específicos para las entradas.

---

## 6. Próximos Pasos

### 6.1. Añadir Proyectos

Tengo planeado añadir una sección para mostrar mis proyectos. Esto incluirá una breve descripción de cada proyecto, tecnologías utilizadas y enlaces relevantes.

### 6.2. Separación de Estilos para Tipos de Blogs

Estoy considerando separar los estilos para los blogs de tipo **técnico** de los blogs más **contemplativos**. Esto permitirá una experiencia de lectura más adecuada para cada tipo de contenido.

---

## Conclusión

Estos cambios han mejorado significativamente la estructura y organización de mi blog. Aunque aún hay trabajo por hacer, estoy satisfecho con el progreso y emocionado por las próximas actualizaciones.

¡Gracias por leer! Si tienes alguna sugerencia o comentario, no dudes en compartirlo.
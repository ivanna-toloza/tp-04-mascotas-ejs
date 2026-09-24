# Trabajo práctico 04 - Aplicación web con EJS (Mascotas)

## Descripción
Esta aplicación web desarrollada con **Node.js**, **Express** y **EJS** gestiona un catálogo de mascotas en adopción. Ofrece una interfaz renderizada en el servidor para listar animales disponibles, consultar su detalle y registrar nuevas mascotas mediante un formulario.

## Instalación
1. Clonar el repositorio.
2. Ejecutar el comando para instalar las dependencias:

```bash
npm install
```

```bash
npm run check
```

1. Diferencia entre Layout, Vista y Parcial
Layout: Estructura global HTML común a todas las páginas de la aplicación.

Vista: Contenido específico asociado a una ruta concreta que reemplaza a <%- body %>.

Parcial: Un módulo reutilizable de HTML (ej: encabezado o pie de página) insertado dentro del layout o de una vista mediante <%- include(...) %>.

2. Datos enviados a una vista mediante res.render
Los objetos pasados como segundo argumento en res.render("vista", { propiedad: valor }) se convierten en variables locales accesibles dentro de la plantilla EJS mediante las etiquetas <%= %> o <% %>.

3. Función de express.static
express.static es un middleware de Express que permite exponer de manera pública carpetas con archivos estáticos (imágenes, CSS, scripts client-side) omitiendo la palabra public en las URLs de solicitud.

4. Función de express.urlencoded
express.urlencoded({ extended: false }) es un middleware encargado de interceptar el cuerpo de las peticiones HTTP realizadas desde formularios HTML tradicionales y transformar la cadena codificada en un objeto JavaScript accesible en req.body.

5. Recorrido POST, Redirección y GET
Cuando el cliente envía datos válidos mediante POST /mascotas, el servidor procesa y guarda la información en la colección en memoria y responde con un código de redirección HTTP 302 hacia /mascotas. El navegador realiza automáticamente una nueva solicitud GET /mascotas, lo que evita la re-ejecución accidental del envío de datos si el usuario recarga la página.

6. Motivo por el cual el nuevo registro desaparece al reiniciar
La modificación efectuada por POST se realiza únicamente sobre el arreglo en la memoria RAM. El archivo original datos/mascotas.json en el disco jamás se modifica. Como la RAM es volátil, al detener el proceso y ejecutar de nuevo npm start, Node.js vuelve a leer el archivo físico restaurando el estado original.
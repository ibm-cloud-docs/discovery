---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Comprensión de documentos inteligentes

La comprensión de documentos inteligentes (SDU) es una nueva forma de anotar los documentos en {{site.data.keyword.discoveryfull}}. 

El editor facilita el entrenamiento de modelos de conversión personalizados. Personalizar cómo se indexan los documentos en Discovery mejorará las respuestas devueltas en su aplicación.

La comprensión de documentos inteligentes está en versión release beta. Encontrará una explicación de las características beta que puede encontrar [aquí](/docs/services/discovery/release-notes.html#beta-features).

## Navegadores y tipos de documentos soportados
{: #doctypes}

Tipos de documentos soportados: PDF, Word, HTML. {{site.data.keyword.discoveryfull}} soporta documentos JSON, pero estos no se abren en el editor de la comprensión de documentos inteligentes porque son documentos estructurados.

Navegadores soportados para este release beta: Chrome y Firefox.

## Cómo anotar los documentos
{: #annotate}

Para abrir el editor de comprensión de documentos inteligentes:

1. Abra {{site.data.keyword.discoveryfull}} utilizando el enlace beta.
1. Abra una recopilación de datos privados y en la pantalla **Gestionar datos**, pulse **Ir a valores de datos**. 
1. En la pantalla **Valores de datos**, encontrará dos separadores: **Extraer campos** y **Enriquecer campos**.

   - **Extraer campos** contiene el editor de comprensión de documentos inteligentes. Este separador sustituye los separadores **Convertir** y **Normalizar** de la pantalla de {{site.data.keyword.discoveryshort}} original. 
   - El separador **Enriquecer campos** es idéntico a **Enriquecer** en la pantalla original. Para obtener más información sobre los enriquecimientos, consulte [Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments). La opción **Cargar documentos de ejemplo** no está disponible en **Enriquecer campos**, porque no es necesaria.

1. Veinte (20) documentos de la recopilación se cargarán automáticamente en el separador **Extraer campos**, en el editor de Comprensión de documentos inteligentes.

La barra de herramientas de la parte superior le permitirá:
- Seleccionar un documento
- Navegar por el documento mostrado
- Ajustar la vista de página (`vista de página única`, `acercar`, `alejar`), `borrar cambios` y `exportar/importar modelos`. Pulse en `vista de página única` para conmutar a una pantalla que mostrará las anotaciones y el documento por separado. 

### Anotación de un documento en el editor de Comprensión de documentos inteligentes
{: #documents}

**Nota:** Las tablas se anotan en un paso aparte.

Consulte [Prácticas recomendadas para etiquetar documentos y tablas](/docs/services/discovery/sdu.html#bestpractices) antes de empezar a realizar anotaciones.

1. Aparecerá un grupo de campos predeterminado en la parte derecha del documento. (Para la versión beta, no puede crear campos personalizados, pero esta característica estará disponible en el futuro). Los campos disponibles son `respuesta`, `autor`, `pie-de-página`, `cabecera`, `pregunta`, `subtítulo`, `tabla-de-contenidos`, `texto` y `título`.
1. Pulse en el nombre del campo en la parte derecha para activarlo.
1. Haga clic en el contenido que representa este campo en el editor de Comprensión de documentos inteligentes. Aparecerá resaltado. 
   - De forma alternativa, puede seleccionar un nombre de campo de la derecha y arrastrarlo al contenido en el editor de Comprensión de documentos inteligentes. 
   - Para borrar un cambio, pulse en el botón **Borrar cambio** en la barra de herramientas.
1. Pulse **Enviar**.
   **Nota:** A medida que realiza anotaciones, Watson aprende y empieza a predecir anotaciones. Siga realizando anotaciones hasta que Watson identifique los campos de forma correcta y coherente.
1. Cuando haya terminado de realizar anotaciones, pulse en **Aplicar cambios a la recopilación**. Se abrirá la pantalla **Cargar los documentos**. (Esto cambiará después de la beta). Ahora podrá cargar los documentos para que los valores actualizados se apliquen a toda la recopilación. Cuando se haya completado la carga, se le redirigirá a la pantalla **Gestionar datos**.


Campo | Definición  
------ | ------ 
respuesta | En un par de pregunta/respuesta (normalmente en las preguntas más frecuentes), la respuesta a la pregunta.
autor | Nombre del autor (o autores).
pie-de-página | Utilice este separador para denotar metainformación sobre el documento (como el número de página o referencia) que aparecen en la parte inferior de la página.
cabecera | Utilice esta etiqueta para indicar metainformación sobre el documento que aparece en la parte superior de la página.
pregunta | En el par de preguntas/respuestas (normalmente en las preguntas más frecuentes), la pregunta.
subtítulo | El título secundario del documento que se está anotando. Utilice esta etiqueta solo una vez por documento.
tabla-de-contenidos | Utilice esta etiqueta en las listas de la tabla de contenido del documento.
texto | Utilice esta etiqueta en el texto de copia estándar, incluidos parágrafos, definiciones o cualquier grupo de palabras que no sean un título, parte de una tabla, una respuesta, un autor, un subtítulo o un pie de página. 
título | El título principal del documento que se está anotando. Utilice esta etiqueta solo una vez por documento.

### Anotación de una tabla en el editor de Comprensión de documentos inteligentes
{: #tables} 

1. Seleccione el campo `table` en la parte derecha y elija la tabla en el editor de Comprensión de documentos inteligentes. 
1. Mueva el puntero del ratón sobre la tabla del editor de la Comprensión de documentos inteligentes para visualizar el botón **Anotar tabla**. Pulse en el botón para abrir el editor de tablas.
1. Primero, realice un esquema de la tabla:
   - Seleccione el campo `columna`.
   - Pulse en una columna de la tabla para activarla.
   - Seleccione el campo `fila`.
   - Pulse en una fila de la tabla para activarla.

   El esquema de la tabla aparecerá en la vista previa de la tabla en la parte izquierda.

   **Nota:** Puede pulsar en **Predecir**para ver una predicción de modelo de la anotación de la tabla.
1. En segundo lugar, etiquete el contenido de la tabla.
1. Cuando haya terminado de realizar anotaciones en la tabla, pulse en **Anotaciones terminadas**.
1. Pulse en **Aplicar cambios a la recopilación**. Se abrirá la pantalla **Cargar los documentos**. (Esto cambiará después de la beta). Cuando se haya completado la carga, se le redirigirá a la pantalla **Gestionar datos**.

Campo | Definición  
------ | ------ 
cuerpo de tabla | Cualquier celda sin cabecera que contenga información
cabecera de columna | La celda de cabecera (si está presente) de cada columna de la tabla 
cabecera de varias columnas | Cualquier celda de cabecera que abarque más de una columna
título de la subsección | La cabecera de columna para la columna de las cabeceras de fila (si están presentes)
cabecera de filas | La etiqueta de fila (si está presente) de cada fila de la tabla
cabecera de varias filas | Cualquier etiqueta de fila que abarque más de una fila

## Prácticas recomendadas para etiquetar documentos y tablas
{: #bestpractices}

- Siga todas las directrices y cree etiquetas de forma coherente en todos los documentos
- No etiquete espacios en blanco
- No etiquete diagramas e imágenes
- No trate el texto en **negrita**, _cursiva_ o subrayado de forma distinta, cree las etiquetas en función del contexto, no del estilo. 
- Al etiquetar un documento, hágalo de la primera página a la última. Es necesario enviar todas las páginas, aunque no se haya creado ninguna etiqueta. 
- Si etiqueta un elemento de manera incorrecta, seleccione primero otra etiqueta para que el elemento se sobrescriba.
- Se pueden enviar las páginas en cualquier momento. Asegúrese de haber completado todo el proceso de etiquetado antes de enviarlas.
- No utilice la función de zoom en el navegador cuando etiquete documentos.
- Los documentos y tablas que parecen tener texto superpuesto a otro texto se conocen como documentos y tablas con "superposición doble" y no se pueden anotar. Notifique a su administrador acerca de estos documentos.
- Los documentos y tablas que contienen varias columnas de texto en una sola página no se pueden anotar. Notifique a su administrador acerca de estos documentos.
- Las notas a pie de página deben marcarse solo cuando aparezcan en la parte inferior de la página y estén referenciadas en el cuerpo de texto principal del documento.
- Las notas que aparezcan en las secciones o listas (por ejemplo, las llamadas de forma explícita "Notas") deben etiquetarse como `texto`.
- Si no está seguro de que la tabla se haya etiquetado correctamente y el panel de vista previa no responde, será necesario volver a cargar la página en el navegador y etiquetar la tabla para garantizar que se haya corregido la etiqueta.


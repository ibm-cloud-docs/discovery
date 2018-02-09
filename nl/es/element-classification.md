---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

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

# Clasificación de elementos
{: #element-classification}

La clasificación de elementos permite analizar rápidamente los documentos normativos para convertir, identificar y clasificar elementos de importancia. Con la ayuda de la última tecnología del NLP (Natural Language Processing), es posible extraer de elementos del documento la parte (a quién se refiere el documento), la naturaleza (el tipo del elemento) y la categoría (clase específica). 

La clasificación de elementos está diseñada para proporcionar:

- Entendimiento del lenguaje natural de contratos, con un interés especial en contratos de suministros de software y en documentos sobre regulaciones
- La posibilidad de convertir PDF programático en JSON anotado
- Identificación de categorías y entidades legales que se alinean con el área de conocimiento del tema

La clasificación de elementos reúne también un amplio conjunto de funcionalidades de API integradas y automatizadas de Watson para especificar como entrada PDF programáticos para identificar: secciones, listas (numeradas o con viñetas), notas de pie de página y tablas; convirtiendo estos elementos en un formato HTML estructurado. Además, la clasificación de este formato estructurado se anota y explicita como JSON con categorías, tipos y elementos anotados. 

La clasificación de elementos transmite los datos de forma segura al cifrarlos mientras se transiten o cuando están en reposo. Para obtener información sobre la seguridad de IBM Cloud, consulte [Descripción del servicio IBM Cloud Service ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}.

## Requisitos de clasificación 

Para clasificar documentos mediante la clasificación de elementos, la configuración y los documentos de origen deben cumplir los siguientes requisitos:

- Los archivos a analizar deben estar en formato PDF.
- El contenido del PDF debe estar en forma de texto (documentos escaneados, sin que se hayan reconocido sus caracteres no se pueden analizar). 

  **Nota:** Puede identificar si un PDF posee texto abriendo el documento en un visor de PDF y utilizando la herramienta **Seleccionar texto** para seleccionar una única palabra. Si no puede seleccionar una única palabra en el documento, el archivo no se puede analizar.

- Los archivos no pueden tener un tamaño superior a 50Mb. 
- No es posible analizar PDF protegidos (con una contraseña para poder abrirlos) y cuya edición esté restringida (con una contraseña para poder editarlos).  
- Se debe crear una configuración personalizada de {{site.data.keyword.discoveryshort}} que incluya el enriquecimiento de `elements`. Esta configuración solo se puede utilizar para ingerir documentos PDF. 
- Los planes **Lite** y **Standard** permiten procesar un máximo de 500 páginas por mes. 
- No está disponible para instancias de servicio suscritas al plan **Premium**. 

## Requisitos de recopilación

Para utilizar la clasificación de elementos, la recopilación se debe configurar para satisfacer los siguientes requisitos: 

- Los valores de conversión de `PDF` se ignoran si se especifican. 
- Los valores de conversión de `WORD` se pueden omitir puesto que los archivos de Microsoft Word no se pueden ingerir cuando se especifica la clasificación de elementos. 
- Los valores de normalización de `html` se ignoran si se especifican. 
- La división de documentos no está soportada cuando se especifica el enriquecimiento de `elements`. 
- En la configuración de {{site.data.keyword.discoveryshort}}, el campo `html` se debe enriquecer con el enriquecimiento `elements` y el `model` especificado como `contract`. En el siguiente ejemplo, `destination_field` es `enriched_html`, pero se puede utilizar cualquier otro valor válido: 

```json
"enrichments": [
  {
    "source_field": "html",
    "destination_field": "enriched_html",
    "enrichment": "elements",
    "options": {
      "model": "contract"
    }
  }
]
```
{: codeblock}

Estas opciones se pueden añadir con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, creando una configuración personalizada y añadiendo el enriquecimiento **Clasificación de elementos** al campo `html`. 

**Nota:** Al añadir la **Clasificación de elementos** utilizando el conjunto de herramientas, `destination_field` se establece en `enriched_html_elements`. 

Después de que se haya creado la configuración personalizada, está puede ser utilizada en cualquier recopilación y método para cargar documentos siempre que se especifique dicha configuración personalizada. Si no está familiarizado con la creación de recopilaciones y la carga de documentos, consulte [Iniciación al conjunto de herramientas](/docs/services/discovery/getting-started-tool.html).  

## Elementos clasificados

Una vez que un documento se ha indexado con la clasificación de elementos, será devuelto con una matriz `elements` como parte del documento en el que se podrán realizar búsquedas. 

Cada objeto de la matriz `elements` describe un elemento del contrato que la clasificación de elementos ha identificado. El código siguiente representa un elemento típico:

```
{
   "sentence" : {
     "begin" : 34941,
     "end" : 35307
   },
   "sentence_text" : "A buyer must buy from the supplier.",
   "types" : [ {
     "label" : {
       "nature" : "Obligation",
       "party" : "Supplier"
     },
     "assurance" : "High"
   } ],
   "categories" : [ {
     "label : "Responsibilities",
     "assurance : "High"
     }
   ]
}
```

Hay las siguientes secciones importantes en el elemento:

- `sentence_text` – el texto analizado. 
- `sentence` - este objeto describe dónde se encontró el elemento en el HTML convertido, contiene un valor de carácter de inicio y un valor de carácter final. 
- `types` – esta matriz describe lo qué es el elemento y a quién afecta. Esta formada por uno o varios conjuntos de `party` (quién está siendo afectado por la frase) y la `nature` (el efecto de la frase en la parte identificada)
- `categories` - esta matriz enumera las categorías funcionales en las que se incluye la frase identificada. El tema de la frase. 

**Nota**: Algunas frases no caen dentro de una categoría o tipo, en cuyo caso las matrices `types` y `categories` se devuelven vacías. 

**Nota**: Algunas frases abarcan varios temas por lo que serán devueltas listando varios elementos de `types` y `categories`. 

Además, las partes identificadas también se definirán en la matriz de partes: 

```
  "parties" : [ {
    "party" : "Customer",
    "role" : "Buyer"
  } ]
```

Hay dos secciones importantes para cada elemento de la matriz de partes:

- `party` - texto que se ha identificado como una parte en el documento.
- `role` – rol de la parte que ha sido identificado. Los roles cambian según el subdominio, consulte la información en el subdominio especificado para obtener una lista de los posibles roles. Las partes que no se pueden identificar con un rol específico se etiquetan como 


## Visión general de los elementos de un contrato

Los contratos analizados desde la clasificación de elementos se devuelven con cada elemento identificado analizado. 

En las siguientes secciones se describe cómo el JSON devuelto describe el análisis. 

### Tipo

La información del elemento `types` es una matriz de objetos, donde cada objeto contiene la naturaliza y la parte identificadas en forma de dupla para este elemento. En las siguientes tablas se describen las posibles `natures` y `parties` que se pueden identificar. 

Las naturalezas son los tipos de acción que la frase requiere.

| **Naturaleza** | **Descripción** |
| --- | --- |
| Definition | Este elemento añade claridad para un término/relación/etc. No es necesaria una acción para cumplimentar este elemento. No hay una parte afectada. |
| Disclaimer | La parte en el elemento no está obligada a cumplir los términos específicos en el elemento, pero no se le impide cumplirlos. |
| Exclusion | La parte en el elemento no satisfará los términos específicos presentados en el elemento. |
| Obligation | La parte en el elemento está obligada a satisfacer los términos del elemento. |
| Right | La parte en el elemento tiene garantizada el cumplimiento de los términos del elemento. |

### Partes

En cada cláusula identificada, las partes afectadas se identifican por su nombre. Cada parte identificada se clasifica posteriormente por su `role`. Las partes son los participantes en el contrato. Los roles que se pueden identificar para los contratos son los siguientes: 

| **Rol** | **Descripción** |
| --- | --- |
| `Buyer` | La parte responsable de pagar los bienes/servicios. |
| `End User` | La parte que interactuará con los bienes/servicios reales, y que se distingue de forma explícita del comprador. |
| `None` | No se ha identificado ninguna parte para este elemento. Siempre se empareja con la definición de la naturaleza. |
| `Supplier` | La parte responsable de proporcionar los bienes/servicios. |

### Categorías

Las categorías definen el tema de la frase. Se pueden identificar las siguientes categorías. 

| **Categorías** | **Descripción** |
| --- | --- |
| `Amendments` | Una modificación del contrato original que establece las condiciones para cambiar los términos. |
| `Asset Use` | Detalles de los activos en el acuerdo que serán utilizados por cualquiera de las partes. |
| `Assignments` | Abarca la transferencia de derechos que posee una parte a otra. |
| `Audits` | Esta cláusula permite que el comprador examine o inspeccione al proveedor de los servicios que se están proporcionando.  |
| `Communication` | Describe los métodos de comunicación aceptables y la información de contacto. |
| `Confidentiality` | Describe cómo se manejará la información confidencial o privado. Por ejemplo, qué se puede compartir, quién lo puede compartir y cómo se puede compartir. |
| `Business Continuity` | Describe cómo una organización continuará la entrega de trabajo en niveles predefinidos, en el caso que se presente un incidente que afecte a dicha entrega. |
| `Definitions` | Una sección que define un término utilizado en el documento. |
| `Deliverables` | Elementos o servicios a entregar al final de una unidad de trabajo. |
| `Delivery` | El proceso o planificación específica para completar un proyecto. |
| `Dispute Resolution` | Para cualquier disputa que pueda surgir entre las partes contratantes, y la forma en la que será manejada dicha disputa. |
| `Force Majeure` | Una cláusula que libera ambas partes de responsabilidad en caso de un suceso de interrupción. |
| `Indemnification` | Describe las acciones a realizar o las consecuencias si se incumplen los términos. |
| `Insurance` | Describe el nivel de cobertura mediante un seguro que debe poseer el suministrador. |
| `Intellectual Property` | Una cláusula que se refiere a las patentes, derechos de autor y marcas. Habitualmente está relacionada con invenciones, derechos de autor y know-how.  |
| `Liability` | Describe las obligaciones y limitaciones en la responsabilidad de cada parte. |
| `Miscellaneous` | Secciones de interés que no se adecúan a otras categorías. |
| `Payment Terms & Billing` | Describe la forma de los pagos y su planificación. |
| `Pricing & Taxes` | Describe la fijación de precios y la forma en la que se aplicarán los impuestos. |
| `Privacy` | Describe las regulaciones de privacidad que se aplicarán. |
| `Responsibilities` | Describe las responsabilidades de cada parte. |
| `Safety and Security` | Describe cómo prevenir daños a una parte. Se incluyen tanto la seguridad de activos físicos como personales. |
| `Scope of Work` | Describe lo que obtendrán las partes y que se detalla en forma de una instrucción de trabajo. |
| `Subcontracts` | Menciona a las terceras partes involucradas para cumplir un requisito. |
| `Term & Termination` | El tiempo de afectación y las condiciones en las que podría finalizar. |
| `Warranties` | Garantía que un proveedor proporciona sobre cómo funcionará un producto. |

### Garantías 

A cada elemento (tipo o categoría) que la clasificación de elementos identifica se le proporciona una valoración de `assurance`. A continuación se describen los siguientes valores de garantía: 

| **Garantía** | **Descripción** |
| --- | --- |
| `High` | Hay una evidencia significativa que la clasificación que se está ofreciendo es representativa del contendido. |
| `Low` | Hay una evidencia parcial que da soporte a la clasificación, sin embargo, podría ser necesaria una revisión adicional para poder confirmarlo. |

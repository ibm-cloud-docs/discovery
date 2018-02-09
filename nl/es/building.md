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

# Configuración del servicio

La creación de un servicio {{site.data.keyword.discoveryshort}} hará posible obtener conocimientos útiles mediante el enriquecimiento de sus propios datos y luego entregarlo en un formato capaz de ser consultado.
{: shortdesc}

Antes de añadir su propio contenido para el servicio {{site.data.keyword.discoveryshort}}, debe configurar el servicio para procesar el contenido de la forma que desea.

El primer paso es configurar los parámetros básicos del servicio ([Preparación del servicio para los documentos](/docs/services/discovery/building.html#preparing-the-service-for-your-documents)), esto incluye la creación de un entorno y la creación de una o varias recopilaciones dentro de dicho entorno. Cuando se crea una recopilación, de forma automática se proporciona un conjunto de valores predeterminados ([La configuración predeterminada](/docs/services/discovery/building.html#the-default-configuration)). Si está satisfecho con estos valores predeterminados, puede proceder a cargar su contenido ([Adición de contenido](/docs/services/discovery/adding-content.html)).

Sin embargo, lo más probable es que desee especificar una o más configuraciones personalizadas (consulte [Cuándo es necesaria una configuración personalizada](/docs/services/discovery/building.html#when-you-need-a-custom-configuration)). Si este es el caso, deberá hacer lo siguiente:

-   Identificar algún contenido de ejemplo (documentos representativos de sus archivos)
-   Cargar el contenido ([Cargar documentos de ejemplo](/docs/services/discovery/building.html#uploading-sample-documents))
-   Ajustar el proceso de conversión ([Conversión de documentos de ejemplo](/docs/services/discovery/building.html#converting-sample-documents))
-   Definir enriquecimientos ([Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments))
-   Normalizar los resultados ([Normalización de datos](/docs/services/discovery/building.html#normalizing-data))

    Después de haber creado la configuración personalizada, puede cargar sus documentos ([Adición de contenido](/docs/services/discovery/adding-content.html)).

## Preparación del servicio para los documentos
{: #preparing-the-service-for-your-documents}

En el servicio {{site.data.keyword.discoveryshort}}, el contenido que carga se almacena en una recopilación que forma parte de su entorno. Debe crear el entorno y la recopilación para poder cargar su contenido.

-   **Entorno** — El entorno define la cantidad del espacio de almacenamiento que tiene para el contenido en el servicio {{site.data.keyword.discoveryshort}}. Es posible crear un máximo de un entorno por cada instancia del servicio {{site.data.keyword.discoveryshort}}. 

    Hay disponibles varios planes (Lite, Standard y Advanced) que puede elegir. Consulte el [Catálogo de {{site.data.keyword.discoveryshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window} para obtener más información. Los archivos de origen no se tienen en cuenta para el límite del tamaño de archivo. 

-   **Recopilación** — Una recopilación es una agrupación de su contenido en el entorno. Se debe crear al menos una recopilación para poder cargar su contenido.

    Las recopilaciones están formadas por sus datos privados, sin embargo, {{site.data.keyword.discoveryshort}} también incluye {{site.data.keyword.discoverynewsshort}}, un conjunto de datos público enriquecido de forma previa. Puede utilizarlo para consultar información: alertas de noticias, detección de sucesos y temas de tendencias, que puede integrar en sus aplicaciones.

    {{site.data.keyword.discoverynewsshort}}, un conjunto de datos públicos que previamente se ha enriquecido con conocimientos cognitivos, también se incluye con {{site.data.keyword.discoveryshort}}. Consulte [Watson Discovery News](/docs/services/discovery/watson-discovery-news.html#watson-discovery-news) para obtener más información. No es posible modificar la configuración de {{site.data.keyword.discoverynewsshort}} o añadir documentos a esta recopilación. Consulte una demostración que puede realizar con {{site.data.keyword.discoverynewsshort}} [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://discovery-news-demo.mybluemix.net/){: new_window}.

Para crear un entorno y una recopilación de datos privados con el conjunto de herramientas de {{site.data.keyword.discoveryshort}} siga estos pasos: 

1.  En la pantalla de **Gestionar datos**, pulse el icono ![Rueda](images/icon_settings.png) y elija **Crear entorno**. El entorno se crea basándose en el plan de {{site.data.keyword.Bluemix_notm}} que haya seleccionado con anterioridad. El estado de su entorno siempre está disponible desde este desplegable. 

1.  Una vez que el entorno esté listo, pulse el botón **Crear una recopilación de datos**. A continuación, puede **Nombrar su nueva recopilación**. 

    De forma predeterminada, el archivo de configuración será la **Configuración predeterminada**. Si tiene otro archivo de configuración disponible, puede elegirlo o puede crear uno nuevo más tarde y aplicarlo a esta recopilación. También se puede seleccionar el idioma de los documentos que se añadirán a esta recopilación: inglés, alemán, español, árabe, francés, italiano, coreano o portugués (Brasil). Debería haber un solo idioma en cada una de sus recopilaciones. Después de pulsar **Crear**, la recopilación de datos aparecerá como un mosaico.

El entorno y la recopilación de datos están listos. Si desea utilizar el archivo de configuración predeterminado, puede iniciar la [Adición de contenido](/docs/services/discovery/adding-content.html) inmediatamente. Pero si desea personalizar su configuración de {{site.data.keyword.discoveryshort}} con enriquecimientos adicionales y valores de conversión, no debería empezar a añadir documentos ahora, sino empezar creando el archivo de configuración personalizada. Consulte [Configuración del servicio](/docs/services/discovery/building.html#custom-configuration).

**Nota:** Cuando se cargan documentos en una recopilación de datos, se convierten y enriquecen utilizando el archivo de configuración elegido para dicha recopilación. Si decide posteriormente que desea cambiar una recopilación con un archivo de configuración diferente, puede hacerlo, sin embargo, los documentos que ya se han cargado seguirán convertidos según al archivo de configuración original. Todos los documentos cargados después de cambiar el archivo de configuración utilizarán el nuevo archivo de configuración. Si desea que **toda**
la recopilación utilice la nueva configuración, necesitará crear una nueva recopilación, elegir el nuevo archivo de configuración y volver a cargar todos los documentos. El servicio {{site.data.keyword.discoveryshort}} almacena el texto convertido de los documentos que ha cargado. No se almacenan ni se devolverán en los resultados las imágenes incluidas en los archivos **PDF** y **Microsoft Word**. 

### La configuración predeterminada
{: #the-default-configuration}

El servicio {{site.data.keyword.discoveryshort}} incluye un archivo de configuración estándar que convertirá, enriquecerá y normalizará los datos sin la necesidad de configurar manualmente estas opciones.

Este archivo de configuración predeterminado se denomina la **Configuración predeterminada**. Contiene enriquecimientos, además de conversiones de documento estándar basado en estilos y tamaños de font. 

Primero los enriquecimientos predeterminados. {{site.data.keyword.discoveryshort}} enriquecerá (añadirá metadatos cognitivos) al campo de texto de sus documentos con información semántica recopilada por los cuatro enriquecimientos de {{site.data.keyword.watson}} -Extracción de entidades, Análisis de sentimientos, Clasificación de categorías, Etiquetado de conceptos (aprenda más sobre los mismos [aquí](/docs/services/discovery/building.html#adding-enrichments)). 

**Nota:** Desde el **18 de julio del 2017** {{site.data.keyword.discoveryfull}} introdujo una nueva tecnología de enriquecimiento, denominado el NLU ({{site.data.keyword.nlushort}}). Consulte [Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments) para obtener más información. Si aplicó la **Configuración predeterminada** a una recopilación antes de esta fecha, dicha recopilación se enriqueció con los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}. Si aplicó la **Configuración predeterminada** a una recopilación después de esta fecha, se utilizarán los enriquecimientos de {{site.data.keyword.nlushort}}. 

-   [Conversión de Microsoft Word ](/docs/services/discovery/building.html#microsoft-word-conversion)
-   [Conversión de PDF](/docs/services/discovery/building.html#pdf-conversion)
-   [Conversión de HTML](/docs/services/discovery/building.html#html-conversion)
-   [Conversión de JSON ](/docs/services/discovery/building.html#json-conversion)

Si desea crear una configuración personalizada, consulte [Configuración personalizada](/docs/services/discovery/building.html#custom-configuration).

### Cuándo se necesita una configuración personalizada
{: #when-you-need-a-custom-configuration}

La obtención de la información correcta a partir de su contenido y su entrega a sus objetivos es el objetivo del servicio {{site.data.keyword.discoveryshort}}. La configuración que se utiliza para ingerir el contenido identifica la información y cómo esta se almacena. Los tipos de contenido que el servicio {{site.data.keyword.discoveryshort}} puede ingerir son flexibles, lo que significa que aunque el contenido no estructurado esté guardado en un formato específico, no es necesario que la estructura del contenido coincida con la estructura de otro contenido del mismo tipo. 

-   **Entiendo que es posible que mis documentos no estén estructurados de la misma forma que la configuración predeterminada espera. *¿Cómo sé si los valores predeterminados son los adecuados para mi caso?***
    -   La manera más fácil de ver si la configuración predeterminado es la adecuada para mi caso es [Cargar documentos de ejemplo](/docs/services/discovery/building.html#uploading-sample-documents). Si los resultados del JSON de ejemplo satisfacen sus expectativas, entonces no se necesita ninguna configuración adicional.
-   **Entiendo que se añaden enriquecimientos predeterminados al campo de texto de mis documentos. ¿Puedo añadir enriquecimientos adicionales para otros campos? **
    -   Desde luego, puede añadir enriquecimientos adicionales a todos los campos que desee. Consulte [Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments) para obtener más información. 

## Configuración personalizada
{: #custom-configuration}

Para crear una configuración personalizada en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, abra una recopilación de datos privados, y en la pantalla **Gestionar datos**, pulse **Conmutar** junto al nombre de la **Configuración**. En el diálogo **Conmutar configuración**, pulse **Crear una nueva configuración**.

Después de haber denominado el nuevo archivo de configuración, dicho nombre se visualizará en la parte superior de la pantalla de configuración. Este nuevo archivo de configuración de forma automática contendrá los valores y los enriquecimientos del archivo de la [Configuración predeterminada](/docs/services/discovery/building.html#the-default-configuration) para que los utilice como punto de partida. 

Los tres pasos para personalizar un archivo de configuración son: **Convertir**, **Enriquecer** y **Normalizar**.

1.  [Conversión de documentos de ejemplo](/docs/services/discovery/building.html#converting-sample-documents)
1.  [Adición de enriquecimientos](/docs/services/discovery/building.html#adding-enrichments)
1.  [Normalización de datos](/docs/services/discovery/building.html#normalizing-data)

### Cargar documentos de ejemplo
{: #uploading-sample-documents}

Para que el proceso de configuración sea más eficiente, puede cargar hasta diez archivos Microsoft Word, HTML, JSON, o PDF que sean representativos de su conjunto de documentos. Son los denominados **documentos de ejemplo**. Los documentos de ejemplo no se añaden a la recopilación, sólo se utilizan para identificar campos que son comunes a los documentos y para personalizar los campos de acuerdo con sus requisitos.

Al crear un nuevo archivo de configuración en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, puede cargar documentos de ejemplo a través del mecanismo de arrastrar y soltar o examinando los archivos a través de su sistema de archivos. Pulse en el nombre de archivo en el panel **Cargar documentos de ejemplo** para obtener una vista previa de cada archivo. 

#### Recuerde los siguientes aspectos al cargar documentos de ejemplo:

-   Todos los documentos se convierten a JSON antes de ser enriquecidos e indexados. 
-   Los documentos Microsoft Word y PDF se convierten primero a documentos HTML y, a continuación a JSON. 
-   Los documentos HTML se convierten directamente a JSON.
-   El tamaño máximo del archivo como documento de ejemplo es de 5MB. Los documentos de ejemplo se suprimen automáticamente después de 1 mes, pero los puede cargar de nuevo si desea realizar cambios adicionales a su configuración. 

#### Directrices para elegir buenos documentos de ejemplo:

-   Debe tener (como mínimo), un documento de ejemplo para cada tipo de archivo desea ingerir - Microsoft Word, PDF, HTML y JSON.
-   Si tiene tipos de documento únicos (por ejemplo, informes financieros o notas de prensa), incluya uno de cada tipo en su conjunto de documentos de ejemplo. 
-   Con documentos HTML, debería elegir documentos que incluyan etiquetas HTML que desearía excluir, así como atributos de etiquetas que desearía incluir o excluir. 
-   Los documentos JSON deberían incluir los campos que desea eliminar o fusionar (por ejemplo, zipCode y postalCode). 

### Conversión de documentos de ejemplo
{: #converting-sample-documents}

La conversión de los documentos de ejemplo es el proceso que permitirá definir la forma en la que se manejará cada tipo de entrada. El tipo de archivo del contenido que carga determina el número de pasos de conversión que considerará. 

Antes de empezar, [cargue sus documentos de ejemplo](/docs/services/discovery/building.html#uploading-sample-documents), y abra un documento de ejemplo del tipo de archivo que desea configurar en el panel de la derecha. 

Para trabajar con los valores de conversión, pulse a través de los tipos de archivo. 

![Conversión de un documento de ejemplo](images/convert.png)

-   **Si está convirtiendo archivos de Microsoft Word debe hacer lo siguiente:**
    -   Establezca las opciones de conversión de Microsoft Word
    -   Establezca las opciones de conversión de HTML
    -   Establezca las opciones de conversión de JSON
    -   Revise el resultado

-   **Si está convirtiendo archivos PDF debe hacer lo siguiente:**
    -   Establezca las opciones de conversión de PDF
    -   Establezca las opciones de conversión de HTML
    -   Establezca las opciones de conversión de JSON
    -   Revise el resultado

-   **Si está convirtiendo archivos HTML debe hacer lo siguiente:**
    -   Establezca las opciones de conversión de HTML
    -   Establezca las opciones de conversión de JSON
    -   Revise el resultado

-   **Si está convirtiendo archivos JSON** debe establecer las opciones de conversión JSON y revisar el resultado.

Para cada archivo de configuración que cree, sólo hay un conjunto de opciones de conversión para cada paso del proceso. Esto significa que las opciones de conversión de HTML serán las mismas para archivos PDF, Word y HTML. Si necesita opciones de conversión diferentes para cada tipo de contenido que ingerirá (o si tiene archivos del mismo tipo que requerirán diferentes tipos de conversión) deberá almacenar los archivos en distintas recopilaciones y crear archivos de configuración independientes para cada conjunto de valores de conversión. 

#### Conversión de Microsoft Word
{: #microsoft-word-conversion}

Los estilos y tamaños de font de Microsoft Word se utilizan para convertir adecuadamente las cabeceras en los documentos en etiquetas H1, H2, etc. Las etiquetas H1 corresponden al título del documento y las H2 e inferiores son subcabeceras. Utilice los recuadros de texto y los botones de selección para cambiar los valores predeterminados si así lo desea. También puede añadir niveles adicionales de cabeceras y estilos de Word. Si sus documentos de Word tienden a utilizar un nombre de estilo o font específicos para las cabeceras, asegúrese de añadir dicha información. Esto ayudará a mejorar la conversión, lo que dará lugar a mejores resultados de consultas. 

**Ejemplo:** Si es habitual que sus documentos de Word utilicen un font de 20 pt con cursiva para segundas cabeceras, cambie el **Rango de tamaño de font** en **20** a **23** y el **Estilo de font** a **cursiva**.   

Después de realizar los cambios, pulse **Aplicar y guardar**.

#### Conversión de PDF
{: #pdf-conversion}

Los nombres y tamaños de font PDF se utilizan para convertir adecuadamente las cabeceras en los documentos en etiquetas H1, H2, etc. Las etiquetas H1 corresponden al título del documento y las H2 e inferiores son subcabeceras. Utilice los recuadros de texto y los botones de selección para cambiar los valores predeterminados si así lo desea. También puede añadir niveles adicionales de cabeceras. Si sus documentos PDF tienden a utilizar un font específicos para las cabeceras, asegúrese de añadir dicha información. Esto ayudará a mejorar la conversión, lo que dará lugar a mejores resultados de consultas. 

**Ejemplo: ** Si es habitual que sus documentos PDF utilicen un font de 20 pt y negrita para las primeras cabeceras, cambie el **Rango de tamaño de font** en **20** a **80** y el **Estilo de font** a **negrita**. Ajuste los otros niveles según corresponda. 

Después de realizar los cambios, pulse **Aplicar y guardar**.

#### Conversión de HTML
{: #html-conversion}

Puede utilizar este paso para eliminar etiquetas y otra información innecesaria del documento para conservar únicamente la información que necesita para sus consultas. 

Valores HTML predeterminados: 

- Excluir estas etiquetas, así como su contenido: **`script`**, **`sup`**
- Excluir estas etiquetas, pero conservar su contenido:
**`font`**, **`em`**, **`span`**
- Mantener estos atributos de etiqueta: no hay un valor predeterminado
- Excluir estos atributos de etiqueta: **`EVENT_ACTIONS`**
- Mantener el contenido que coincide con este(os) XPath(s): no hay un valor predeterminado 
- Excluir el contenido que coincide con este(os) XPath(s): no hay un valor predeterminado 

Después de realizar los cambios, pulse **Aplicar y guardar**.

#### Conversión de JSON
{: #json-conversion}

El último paso de la conversión es garantizar que el JSON convertido (o cargado) se cree acuerdo a la forma que espera antes de aplicar enriquecimientos al contenido. Se pueden crear reglas que {{site.data.keyword.watson}} utilizará para convertir el HTML en JSON.

-   Se pueden mover, fusionar, copiar o eliminar campos. Por ejemplo, podría desear fusionar **`zipCode`** y **`postalCode`** porque son dos términos similares para el mismo campo. 
-   Los campos vacíos (campos que no contienen información) se suprimirán de forma predeterminada. Es posible cambiar este comportamiento con el conmutador **Eliminar campos vacíos**. 

Después de realizar los cambios, pulse **Aplicar y guardar**.

## Adición de enriquecimientos
{: #adding-enrichments}

**Nota:** Desde el **18 de julio del 2017** {{site.data.keyword.discoveryfull}} introdujo una nueva tecnología de enriquecimiento, denominado el NLU ({{site.data.keyword.nlushort}}). Estos enriquecimientos son los mismos que los enriquecimientos existentes pero requieren una configuración y un esquema ligeramente diferente. Los enriquecimientos originales, denominados enriquecimientos de {{site.data.keyword.alchemylanguageshort}}, pasarán a estar en desuso. El soporte para los enriquecimientos de {{site.data.keyword.alchemylanguageshort}} finalizará el **15 de enero de 2018**. Debería enriquecer las nuevas recopilaciones con {{site.data.keyword.nlushort}} y migrar lo antes posible todas las recopilaciones existentes con archivos de configuración de {{site.data.keyword.alchemylanguageshort}}. Para obtener información sobre la migración de recopilaciones y de archivos de configuración que utilizan los enriquecimientos de {{site.data.keyword.alchemylanguageshort}}, consulte [Migración de enriquecimientos a {{site.data.keyword.nlushort}}](/docs/services/discovery/migrate-nlu.html). 

La [configuración predeterminada](/docs/services/discovery/building.html#the-default-configuration) de {{site.data.keyword.discoveryshort}} enriquecerá (con metadatos cognitivos) el campo `text` de sus documentos ingeridos con información semántica que se recopila para estas cuatro funciones de {{site.data.keyword.watson}} - Extracción de entidades, Análisis de sentimientos, Clasificación de categorías y Etiquetado de conceptos. (Existen un total de nueve enriquecimientos posibles de {{site.data.keyword.watson}}; el resto son Extracción de palabras clave, Extracción de relaciones, Análisis de emociones, Clasificación de elementos y Extracción de roles semánticos). 

**Importante:** Únicamente se enriquecerán los primeros 50.000 caracteres de cada campo JSON seleccionado para ser enriquecido. 

Puede añadir más enriquecimientos al campo `text`, o enriquecer otros campos. Para hacerlo utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, [cree una configuración personalizada](/docs/services/discovery/building.html#custom-configuration), elija el campo o campos a los que desea añadir un enriquecimiento y selecciónelo de la lista de enriquecimiento disponibles de {{site.data.keyword.nlushort}}: 

### Extracción de entidades
{: #entity-extraction}

Obtenga como resultados elementos como, por ejemplo, personas, lugares y organizaciones que estén presentes en el texto de entrada. La extracción de entidades añade conocimiento semántico al contenido para ayudarle a comprender el tema y el contexto del texto que se está analizando. Las técnicas de extracción de entidades se basan en sofisticados algoritmos estadísticos y en tecnología de proceso de lenguaje natural, y son exclusivos en la industria con su soporte para el análisis multilingüe, desambiguación sensible al contexto y extracción de citas. Consulte [aquí](/docs/services/discovery/entity-types.html) la lista completa de tipos y subtipos de entidad. También es posible crear y añadir un [modelo de entidades personalizado](/docs/services/discovery/building.html#custom-entity-model) con {{site.data.keyword.knowledgestudiofull}}.

Ejemplo de un fragmento de un documento enriquecido con la Extracción de entidades:  

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "entities": [
         {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Acme Corporation",
           "relevance": 0.98389,
           "type": "Company"
           },
           {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Atlanta",
           "relevance": 0.532754,
           "type": "Location",
           "disambiguation": {
             "subtype": [
               "AdministrativeDivision",
               "GovernmentalJurisdiction",
               "OlympicHostCity",
               "PlaceWithNeighborhoods",
               "City"
           ],
               "name": "Atlanta",
               "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
           }
           },
           {
           "count": 1,
           "sentiment": {
             "score": 0
           },
           "text": "Georgia",
           "relevance": 0.469643,
           "type": "Location",
           "disambiguation": {
             "subtype": [
               "StateOrCounty"
           ]
    }
  }
```
{: codeblock}

En el ejemplo anterior, puede consultar el tipo de entidad accediendo a `enriched_text.entities.type`.  

`sentiment` se calcula para los tipos de entidad incluso si no se selecciona el enriquecimiento **sentiment**. Para obtener más información sobre la puntuación del sentimiento, consulte el [Análisis del sentimiento](/docs/services/discovery/building.html#sentiment-analysis). 

Los rangos de puntuación de `relevance` están entre `0.0` y `1.0`. Cuanto mayor es la puntuación, mayor es la relevancia de la entidad. El campo `disambiguation` contiene la información de desambiguación para la entidad, que incluye información de la entidad `subtype` y enlaces a los recursos (si hay). `count` corresponde al número de veces que se menciona la entidad en el documento. 

#### Utilización de un modelo de entidades personalizado
{: #custom-entity-model}

Si desea crear un modelo de enriquecimiento personalizado, puede hacerlo en {{site.data.keyword.knowledgestudiofull}} e importar el modelo en {{site.data.keyword.discoveryshort}} añadiendo el ID en el recuadro `ID de modelo personalizado ID` del conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Para obtener más información sobre la integración con {{site.data.keyword.knowledgestudiofull}}, consulte [Integración con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). El modelo personalizado de {{site.data.keyword.knowledgestudiofull}} prevalecerá sobre el enriquecimiento de Extracción de entidades predeterminado. 

**Nota:** Solo se puede asignar un único modelo de {{site.data.keyword.knowledgestudiofull}} a un enriquecimiento. 

### Extracción de relaciones
{: #relation-extraction}

Reconoce cuándo dos entidades están relacionadas e identifica el tipo de relación. También es posible crear y añadir un [modelo de relaciones personalizado](/docs/services/discovery/building.html#custom-relation-model) con {{site.data.keyword.knowledgestudiofull}}.

Consulte [aquí](/docs/services/discovery/relation-types.html) la lista completa de tipos de relación. 

Ejemplo de un fragmento de un documento enriquecido con la Extracción de relaciones: 

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
  "enriched_text": {
    "relations": [
      {
        "type": "locatedAt",
        "sentence": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
        "score": 0.989245,
        "arguments": [
         {
            "text": "Atlanta",
            "location": [
             94,
             101
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Atlanta"
              }
            ]
         },
          {
            "text": "Georgia",
            "location": [
             103,
             110
            ],
            "entities": [
              {
                "type": "GeopoliticalEntity",
                "text": "Georgia"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
{: codeblock}

En el ejemplo anterior, puede consultar el tipo de relación accediendo a `enriched_text.relations.type`. 

Las entidades relacionadas se listan en `arguments`. Los tipos de entidad que se pueden identificar con el enriquecimiento de Extracción de relaciones se puede encontrar [aquí](/docs/services/discovery/relation-types.html#specific-entity-types). 

Los rangos de `score` van de `0.0` a `1.0`. Cuanto mayor es la puntuación, mayor es la relevancia de la relación. 

#### Utilización de un modelo de relaciones personalizado
{: #custom-relation-model}

Si desea crear un modelo de enriquecimiento personalizado, puede hacerlo en {{site.data.keyword.knowledgestudiofull}} e importar el modelo en {{site.data.keyword.discoveryshort}} añadiendo el ID en el recuadro `ID de modelo personalizado ID` del conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Para obtener más información sobre la integración con {{site.data.keyword.knowledgestudiofull}}, consulte [Integración con {{site.data.keyword.knowledgestudiofull}}](/docs/services/discovery/integrate-wks.html#integrating-with-watson-knowledge-studio). El modelo personalizado de {{site.data.keyword.knowledgestudiofull}} prevalecerá sobre el enriquecimiento de Extracción de relaciones predeterminado. 

**Nota:** Solo se puede asignar un único modelo de {{site.data.keyword.knowledgestudiofull}} a un enriquecimiento. 

### Extracción de palabras clave
{: #keyword-extraction}

Los temas importantes de su contenido habitualmente se utilizan al indexar datos, generar nubes de etiquetas o al realizar búsquedas. El servicio {{site.data.keyword.discoveryshort}} automáticamente identifica los idiomas soportados en el contenido de entrada, y luego identifica y clasifica las palabras en ese contenido. 

Ejemplo de un fragmento de un documento enriquecido con la Extracción de palabras clave: 

```json
  {
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "keywords": [
        {
          "text": "Acme Corporation",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.985203
        },
        {
          "text": "new factory",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.821033
        },
        {
          "text": "stockholders",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.66497
        },
        {
          "text": "title",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.332438
        },
        {
          "text": "Atlanta",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.307723
        },
        {
          "text": "Georgia",
          "sentiment": {
            "score": 0
          },
          "relevance": 0.306485
        }
      ]
    }
  }
```
{: codeblock}

En el ejemplo anterior, podría consultar el texto de las palabras claves accediendo a `enriched_text.keywords.text`.  

`sentiment` se calcula para las palabras clave incluso si no se selecciona el enriquecimiento **sentiment**. Para obtener más información sobre la puntuación del sentimiento, consulte el [Análisis del sentimiento](/docs/services/discovery/building.html#sentiment-analysis). 

Los rangos de puntuación de `relevance` están entre `0.0` y `1.0`. Cuanto mayor es la puntuación, mayor es la relevancia de la palabra clave. 

### Clasificación de categorías

Clasifica según categorías el contenido del texto de entrada, HTML o basado en la web en una taxonomía jerárquica de hasta cinco niveles de profundidad. Niveles más profundos permiten clasificar el contenido en subsegmentos más precisos y útiles. Consulte [aquí](/docs/services/discovery/categories.html) la lista completa de categorías. 

Ejemplo de un fragmento de un documento enriquecido con la Clasificación de categorías: 

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "categories": [
        {
          "score": 0.361614,
          "label": "/business and industrial"
        },
        {
          "score": 0.329377,
          "label": "/business and industrial/company/merger and acquisition"
        },
        {
          "score": 0.154254,
          "label": "/business and industrial/business operations/business plans"
        }
      ]
```
{: codeblock}

En el ejemplo anterior, podría consultar el texto de la etiqueta de la categoría accediendo a `enriched_text.categories.label`. 

La etiqueta `label` corresponde a la categoría detectada. Los niveles de jerarquía se separan con barras inclinadas. `score` para la categoría estará en el rango de `0.0` a `1.0`. Cuanto mayor es la puntuación, mayor es la confianza en dicha categoría. 

### Etiquetado de conceptos 
{: #concept-tagging}

Identifica los conceptos con los que el texto de entrada está asociado, basándose en otros conceptos y entidades que están presentes en ese texto. El etiquetado de conceptos entiende cómo se relacionan los conceptos y es capaz de identificar conceptos a los que el texto no hace referencia. Por ejemplo, si un artículo menciona el "CERN" e "Higgs boson", las funciones de la Concepts API identificarán el concepto "Large Hadron Collider", incluso si dicho término no está mencionado de forma explícita en la página. El etiquetado de conceptos permite un mayor nivel de análisis de contenido de entrada que la simple identificación de palabras claves. 

Ejemplo de un fragmento de un documento enriquecido con el Etiquetado de conceptos: 

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "concepts": [
        {
          "text": "Acme Corporation",
          "relevance": 0.91136,
          "dbpedia_resource": "http://dbpedia.org/resource/Acme_Corporation"
        },
        {
          "text": "Factory",
          "relevance": 0.886784,
          "dbpedia_resource": "http://dbpedia.org/resource/Factory"
        }
      ]
```
{: codeblock}

En el ejemplo anterior, puede consultar el tipo del texto del concepto accediendo a `enriched_text.concepts.text`

Los rangos de puntuación de `relevance` están entre `0.0` y `1.0`. Cuanto mayor es la puntuación, mayor es la relevancia del concepto. Si existen, se proporcionan enlaces a los recursos. 

### Extracción de roles semánticos

Identifica las relaciones de sujeto, acción y objeto en el contenido de entrada. La información de relación sirve para identificar automáticamente las señales de compra, sucesos clave y otras acciones importantes. 

Ejemplo de un fragmento de un documento enriquecido con la Extracción de roles semánticos: 

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
      "enriched_text": {
      "semantic_roles": [
        {
          "subject": {
            "text": "The stockholders",
            "keywords": [
              {
                "text": "stockholders"
              }
            ]
          },
          "sentence": " The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
          "object": {
            "text": "pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia",
            "keywords": [
              {
                "text": "Acme Corporation"
              },
              {
                "text": "new factory"
              },
              {
                "text": "Atlanta"
              },
              {
                "text": "Georgia"
              }
            ],
            "entities": [
              {
                "type": "Company",
                "text": "Acme Corporation"
              },
              {
                "type": "Location",
                "text": "Atlanta",
                "disambiguation": {
                  "subtype": [
                    "AdministrativeDivision",
                    "GovernmentalJurisdiction",
                    "OlympicHostCity",
                    "PlaceWithNeighborhoods",
                    "CityTown",
                    "City"
                  ],
                  "name": "Atlanta",
                  "dbpedia_resource": "http://dbpedia.org/resource/Atlanta"
                }
              },
              {
                "type": "Location",
                "text": "Georgia",
                "disambiguation": {
                  "subtype": [
                    "StateOrCounty"
                  ]
                }
              }
            ]
          },
          "action": {
            "verb": {
              "text": "be",
              "tense": "past"
            },
            "text": "were",
            "normalized": "be"
          }
        }
      ]
```
{: codeblock}

En el ejemplo anterior, podría consultar el texto del sujeto de la relación accediendo a `enriched_text.relations.subject.text`. 

`sentiment` se calcula para las relaciones clave incluso si no se selecciona el enriquecimiento **sentiment**. Para obtener más información sobre la puntuación del sentimiento, consulte el [Análisis del sentimiento](/docs/services/discovery/building.html#sentiment-analysis). No extraerá `entities` o `keywords` (tal como se muestra en el ejemplo) a no ser que seleccione los enriquecimientos **entity** y **keyword**. Consulte [Extracción de entidades](/docs/services/discovery/building.html#entity-extraction) y [Extracción de palabras clave](/docs/services/discovery/building.html#keyword-extraction) para obtener más información sobre dichos enriquecimientos. 

Las etiquetas `subject`, `action` y `object` se extraen de cada frase que contiene una relación. 

### Análisis de sentimiento
{: #sentiment-analysis}

Identifica la actitud, las opiniones o los sentimientos en el contenido que se está analizando. El servicio {{site.data.keyword.discoveryshort}} calcula un sentimiento global dentro de un documento, el sentimiento para elementos especificados por el usuario, sentimiento a nivel de entidad, sentimiento a nivel de cita, sentimiento bidireccional y sentimiento a nivel de palabras claves. La combinación de estas funciones da soporte a una variedad de casos de uso que van desde la supervisión de medios sociales al análisis de tendencias.

Ejemplo de un fragmento de un documento enriquecido con el Análisis de sentimiento: 

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "sentiment": {
        "document": {
        "score": 0.459813,
        "label": "positive"
  }
}
```
{: codeblock}

En el ejemplo anterior, podría consultar la etiqueta del sentimiento accediendo a `enriched_text.sentiment.document.label`. 

`label` corresponde al sentimiento general del documento (`positive`, `negative` o `neutral`). 
El sentimiento `label` se basa en `score`. Una puntuación de `0.0` indicaría que el documento es `neutral`, un valor positivo indicaría que el documento es `positive`, y un número negativo indicaría que el documento es `negative`. 

### Análisis de emociones 
{: #emotion-analysis}

Detecta el enfado (anger), el disgusto (disgust), el miedo (fear), la alegría (joy) o la tristeza (sadness) que implícita el texto en inglés. El Análisis de emociones puede detectar emociones que se asocian con frases concretas, entidades, palabras claves o puede analizar el tono emocional global del contenido. 

Ejemplo de un fragmento de un documento enriquecido con el Análisis emocional: 

```json
{
  "text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia.",
    "enriched_text": {
      "emotion": {
        "document": {
          "emotion": {
          "disgust": 0.102578,
          "joy": 0.626655,
          "anger": 0.02303,
          "fear": 0.018884,
          "sadness": 0.096802
    }
  }
}
```
{: codeblock}

En el ejemplo anterior, podría consultar la emoción `joy` accediendo a `enriched_text.emotion.document.emotion.joy`. 

El Análisis de emociones analiza el texto y calcula una puntuación para cada emoción (anger, disgust, fear, joy, sadness) en una escala del `0.0` al `1.0`. Si la puntuación de cualquier emoción es `0.5` o superior, indica que se ha detectado la emoción (y cuanto más se encuentre por encima de `0.5`, mayor será su relevancia). En el fragmento que se muestra, `joy` tiene una puntuación por encima de 0,5, lo que indica que {{site.data.keyword.watson}} ha detectado alegría. 

**Nota:** Solo se da soporte en inglés al Análisis de emociones. 

### Clasificación de elementos
{: #elements}

Analiza elementos (frases, listas, tablas) en documentos normativos importantes para clasificar los tipos y categorías. Para obtener más información, consulte [Clasificación de elementos](/docs/services/discovery/element-classification.html).

#### Precios para el enriquecimiento
{: #enrichment-pricing}

La información sobre los precios para el enriquecimiento está disponible en [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/discovery/){: new_window}.

#### Soporte de idioma nacional para los enriquecimientos
{: #enrichment-language-support}

Para obtener información sobre el soporte de idiomas nacionales para el enriquecimiento, consulte [Soporte de idioma nacional de {{site.data.keyword.discoveryshort}}](/docs/services/discovery/language-support.html).

### Diferencias entre entidades, conceptos y palabras clave
{: #udbeck}

A primera vista, los enriquecimientos de **Extracción de entidades**, **Etiquetado de conceptos** y **Extracción de palabras clave** parecen similares. Utilizaremos el texto de los ejemplos de enriquecimiento para mostrar las diferencias entre los mismos. 

```json
"text": "The stockholders were pleased that Acme Corporation plans to build a new factory in Atlanta, Georgia."

("Los accionistas se congratulan de que Acme Corporation tenga planificado construir una
nueva fábrica en Atlanta, Georgia")
```
{: codeblock}

Puesto que el enriquecimiento de **Extracción de entidades** extrae personas, lugares y organizaciones en el texto de entrada, **Extracción de entidades** devuelve los siguientes tipos de entidad: 

```json
"type": "City"
"text": "Atlanta"

"type": "Company"
"text": "Acme"

"type": "StateOrCounty"
"text": "Georgia"
```
{: codeblock}

Puesto que el enriquecimiento de **Etiquetado de conceptos** entiende la forma en la que se relacionan los conceptos, puede identificar conceptos a los que el texto no hace referencia de forma directa. Por ejemplo, si un artículo menciona el "CERN" e "Higgs boson", identificará el concepto "Large Hadron Collider" incluso si dicho término no está mencionado de forma explícita. Puesto que en el texto del documento de ejemplo únicamente hay una frase, no hay conceptos relacionados, de forma que el **Etiquetado de conceptos** devuelve los siguientes conceptos: 

```json
"text": "Acme Corporation"
"text": "factory"
```
{: codeblock}

Puesto que el enriquecimiento de **Extracción de palabras clave** identifica contenido habitualmente utilizado para indexar los datos, generar nubes de etiquetas o realizar búsquedas, la **Extracción de palabras clave** devuelve las siguientes palabras claves: 

```json
"text": "Acme Corporation"
"text": "new factory"
"text": "stockholders"
"text": "Atlanta"
"text": "Georgia"
```
{: codeblock}

Estos enriquecimientos trabajan conjuntamente para ayudarle a crear mejores consultas. 

## Normalización de datos
{: #normalizing-data}

El último paso para personalizar el archivo de configuración es una limpieza final, que se denomina normalización. 

En la sección **Normalizar** del conjunto de herramientas de {{site.data.keyword.discoveryshort}}: 

-   Se pueden mover, fusionar, copiar o eliminar campos. 
-   Los campos vacíos (campos que no contienen información) se suprimirán de forma predeterminada. Es posible cambiar este comportamiento con el conmutador **Eliminar campos vacíos**. 

Después de realizar los cambios, pulse **Aplicar y guardar** y, a continuación **Hecho**. Volverá a la pantalla **Gestionar datos**, donde podrá aplicar esta configuración a la recopilación que elija. 

## Normalización de entidades
{: #normalizing-entities}

### Utilización de selectores CSS para extraer campos
{: #using-css}

Es posible realizar una normalización adicional mediante selectores CSS a través de la Discovery API.

Si está ingiriendo HTML bien formado, lo puede normalizar, utilizar selectores CSS para extraer campos JSON del mismo y, a continuación, aplicar enriquecimientos a los campos extraídos. Edite su archivo de configuración para habilitar esta característica. Concretamente, añada un elemento `extracted_fields` a la jerarquía `conversions/html` y, a continuación, especifique los nombres de campo, los selectores CSS y los tipos de campo, tal como se indica a continuación: 

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      ...
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    ...
    }
  }
}
```
{: codeblock}

Especifique valores para los nuevos campos nuevos de la siguiente manera:

-   `field_name` - El nombre del campo que se añadirá a la salida de JSON. 
-   `CSS_selector_expression` - El selector CSS con relación al que se debe ejecutar la entrada de HTML para extraer los campos. La expresión puede tener uno o varias coincidencias. 

    Selectores CSS válidos son aquellos especificados por el [Analizador JSoup ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://jsoup.org/apidocs/org/jsoup/select/Selector.html){: new_window} y su [sintaxis de selector ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://jsoup.org/cookbook/extracting-data/selector-syntax){: new_window}. En [Selectores comunes](/docs/services/discovery/building.html#common-selectors) se proporciona una breve lista.
-   `field_type`: `array` o `string`. Si no se especifica el tipo de campo, el valor predeterminado es `array`. Tenga en cuenta que el tipo `string` se puede enriquecer, sin embargo, la información almacenada en un `array` no se puede enriquecer a no ser que se extraigan primero los elementos de la matriz en campos de texto. 

**Aviso:** Si un selector encuentra tanto un nodo padre como uno o varios de sus hijos, el contenido de texto de los nodos se duplicará en la salida de JSON. 

**Nota:** Los nombres de campo deben satisfacer las restricciones que se definen en los [Requisitos de nombre de campo](/docs/services/discovery/custom-config.html#field_reqs). 

En el siguiente fragmento JSON se muestra la sección pertinente de la configuración predeterminada en la que se añade la información del selector CSS. 

```json
{
  "name": "Default Configuration",
  "description": "The configuration used by default when creating a new collection without specifying a configuration_id.",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ]
    }
    ...
  }
}
```
{: codeblock}

En el siguiente fragmento se muestra la configuración con un nuevo nombre y una nueva descripción, así como la ubicación donde puede especificar selectores CSS. 

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "{field_name_1}": {
          "css_selector": "{CSS_selector_expression_1}",
          "type": "{field_type}"
        },
        ...
        "{field_name_N}": {
          "css_selector": "{CSS_selector_expression_N}",
          "type": "{field_type}"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Por último, en el siguiente fragmento se muestra el nuevo nombre de configuración y la descripción así como algunos selectores CSS. Los selectores encuentran coincidencias de elementos en un ejemplo de HTML que se describe más adelante en esta página. 

```json
{
  "name": "Extract JSON config",
  "description": "New configuration enabling extraction of JSON fields from HTML",
  "conversions": {
    ...
    "html": {
      "exclude_tags_completely": [
        "script",
        "sup"
      ],
      "exclude_tags_keep_content": [
        "font",
        "em",
        "span"
      ],
      "exclude_content": {
        "xpaths": []
      },
      "keep_content": {
        "xpaths": []
      },
      "exclude_tag_attributes": [
        "EVENT_ACTIONS"
      ],
      "extracted_fields": {
        "chapters": {
          "css_selector": ".chapter",
          "type": "array"
        },
        "authors": {
          "css_selector": ".author"
        },
        "authors_str": {
          "css_selector": ".author",
          "type": "string"
        },
        "comments": {
          "css_selector": "[^comments-content]"
        }
      }
    }
  }
  ...
}
```
{: codeblock}

Si carga el siguiente documento HTML en una recopilación que utilice una configuración actualizada, los selectores CSS buscarán coincidencias de los atributos y valores apropiados en el HTML. 

```html
<html>
  <body>
    <div id="authors">
      <div class="author"><span class="first_name">Jane</span> <span class="last_name">Rain</span></div>
      <div class="author">Joe Snow</div>
  </div>
  <div class="chapter"><h1>The Rain in Spain</h1><p>falls mainly on the plain.</p></div>
  <div class="chapter"><h1>How I Learned to Stop Worrying</h1><p>and love my snowblower.</p></div>
  <span id="comments-section">
    <h4>Comments:</h4>
    <span id="comments-content-1">Rain gives me pain.</span>
    <span id="comments-content-2">All snow must go!</span>
  </span>
</body></html>
```
{: codeblock}

Después de ingerir y enriquecer el código HTML anterior, el servicio {{site.data.keyword.discoveryshort}} devuelve el siguiente JSON: 

```json
{
  "extracted_metadata": { ... },
  "html": "...",
  "text": "...",
  "extracted_fields": {
    "authors": [ "Jane Rain", "Joe Snow" ],
    "authors_str": "Jane Rain\n\nJoe Snow",
    "chapters": [ "The Rain in Spain\n\nfalls mainly on the plain.", "How I Learned to Stop Worrying\n\nand love my snowblower." ],
    "comments": [ "Rain gives me pain.", "All snow must go!" ]
  }
}
```
{: codeblock}

Después de decidir qué elementos HTML desea extraer, puede también modificar el archivo de configuración para especificar los enriquecimientos desea aplicar a los mismos. 

#### Selectores comunes

Algunos selectores CSS comunes incluyen lo siguiente: 

  - `tag` - Encuentra el nombre de `tag`
  - `.class` - Encuentra el valor de `class`
  - `#id` - Encuentra el valor de `id`
  - `[attribute]` - Encuentra cualquier etiqueta con el `attribute` especificado, independientemente de su valor
  - `[attribute=value]` o `[attribute="value"]` - Encuentra el `attribute` y el `value` especificados. 

## División de documentos con segmentación de documento
{: #doc-segmentation}

Puede dividir los documentos Word, PDF y HTML en segmentos de acuerdo con las etiquetas de cabecera HTML. Una vez divididos, cada segmento es un documento separado que se convertirá a JSON y, a continuación, será indexado y enriquecido por separado. Puesto que las consultas devolverán estos segmentos como documentos separados, la segmentación de documentos se puede utilizar para: 

  - Realizar agregaciones de segmentos individuales de un documento. Por ejemplo, su agregación podría contar cada vez que un segmento menciona una entidad específica, en lugar de contarla únicamente una vez para todo el documento. 
  - Realizar un entrenamiento de relevancia de segmentos en lugar de documentos, lo que mejorará la reclasificación de resultados. 

Los segmentos se crean cuando los documentos se convierten a HTML (los documentos de Word y PDF se convierten a HTML antes de ser convertidos a JSON). Los documentos se pueden dividir con base a las siguientes etiquetas HTML: `h1` `h2` `h3` `h4` `h5` y `h6`.

Consideraciones:

  - El número de segmentos por documento se limita a `50`. Cualquier contenido del documento después de los `49` segmentos se almacenará en el segmento `50`. 

  - Cada segmento se tendrá en cuenta con relación al límite de documentos de su plan. 

  - No es posible normalizar datos (consulte [Normalización de datos](/docs/services/discovery/building.html#normalizing-data)) o utilizar selectores CSS para extraer campos (consulte [Utilización de selectores CSS para extraer campos](/docs/services/discovery/building.html#using-css)) al utilizar la segmentación de documentos. 

  - Si un documento ha sido actualizado y es necesario ingerirlo de nuevo, los segmentos suprimidos permanecerán tal cual después de la nueva ingestión. Estos segmentos se deben suprimir de forma manual con la API (consulte [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#delete-doc){: new_window}:). Además, si la actualización del documento ha añadido contenido que creará nuevos segmentos, o se suprime contenido que eliminará segmentos, a cada sección se le asignará un nuevo `document_id`. Si estos segmentos ya se habían clasificado con el entrenamiento de relevancia, será necesario volver a realizar el entrenamiento. En este caso, en lugar de añadir contenido a un documento existente, considere crear un nuevo documento que contenga el nuevo contenido e ingerirlo por separado. En lugar de suprimir segmentos de un documento existente y volver a ingerirlo, suprima estos segmentos con la API. 

  - Los documentos se segmentarán cada vez que se detecte la etiqueta HTML especificada. Por lo tanto, la segmentación podría dar lugar a HTML mal formado puesto que los documentos se podrían dividir antes del cierre de etiquetas y después la apertura de etiquetas. 

  - Los metadatos HTML, PDF y Word no se extrae y no se incluirá en el índice. Además, los metadatos personalizados que se pasan con el documento cargado no se incluirán en el índice. 

### Cómo realizar una segmentación
{: #performing-segmentation}

La segmentación se configura a través de la API en la sección `conversions`. 

```json
{
  "configuration_id": "a23c467d-1212-4b3a-5555-93e788a3622a",
  "name": "Example configuration",
  "conversions": {
    "segment": {
      "enabled": true,
      "selector_tags": ["h1", "h2", "h3", "h4", "h5", "h6"]
    }
  }
}
```
{: codeblock}

`enabled` = `true` activa la segmentación del documento. 

`selector_tags` es una matriz que especifica las etiquetas de cabecera en las que se pueden segmentar los documentos. 

#### Ejemplo

Configuración: 

```json
"conversions": {
  "segment": {
    "enabled": true,
    "selector_tags": ["h1", "h2"]
```
{: codeblock}

Documento HTML original:

```
<html>
 <head>
 </head>
 <body>
  first line
   <div name="section 1">
    <h1>heading 1</h1>
     <div name="section 2">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment.
      <h2>heading 2</h2>
      line under heading 2
     </div>
       <h3>heading 3</h3>
       line under heading 3
   </div>
  last line
 </body>
</html>
```
{: codeblock}

El aspecto del primer segmento de documento será similar a: 

```json
{
  "id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
  "segment_metadata": {
    "parent_id": "94c686c3-a790-4d8d-ba42-2bddf01b311c",
    "segment": 1,
    "total_segments": 3
  },
  "extracted_metadata": {
    "title": "Heading 1",
    "sha1": "45ede479df67d78f2205ea7e714843375d3029c0",
    "filename": "doc-with-different-heading-levels.html",
    "file_type": "html"
  },
  "text": "This is the text that falls under heading 1 and should be therefore split into its own segment.",
  "html": "<div name=\"section 2\">This is the text that falls under <b>heading 1</b> and should be therefore split into its own segment."
}
```
{: codeblock}

Todos los segmentos incluirán un: 

  - `id` - `id` de este segmento. 
  - La sección `segment_metadata` contiene: 
    - `parent_id` - `parent_id` es el identificador del documento original. En el primer segmento, el `id` y el `parent_id` son el mismo. 
    - `segment` - Número de segmento. 
    - `total_segments` - Número total de segmentos en el que se divide el documento. 
  - La sección `extracted_metadata` contiene: 
    - `title` - El campo `title` se extrae del contenido de la etiqueta de la cabecera en dicho segmento (por ejemplo, `Chapter 1`). Si el primer segmento no incluye una etiqueta de cabecera, el `título` será `no-title`.
    - `sha1` - Del documento original. 
    - `filename` - Del documento original. 
    - `file_type` - Del documento original. 
  - Campo `text`
  - Campo `html` 

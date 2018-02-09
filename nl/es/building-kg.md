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

# Watson Discovery Knowledge Graph

Los gráficos de conocimientos van más allá de la información y los datos creando conexiones dentro de los datos a través de documentos y generando nuevo conocimiento. 
IBM proporciona una tecnología de inteligencia artificial que de forma automática crea gráficos de conocimiento personalizados a partir de datos no estructurados extrayendo y desambiguando entidades y relaciones, enriqueciendo las relaciones con la ayuda de técnicas algorítmicas y clasificando los resultados utilizando algoritmos de relevancia. Los gráficos de conocimiento pueden funcionar como el "centro de conocimientos" de su empresa y se pueden utilizar para la búsqueda empresarial, para resumir información, para motores de recomendación y para otros procesos de toma de decisiones como, por ejemplo, la detección de fraudes, despilfarros o abusos. La utilización de un modelo personalizado (que se crea en {{site.data.keyword.knowledgestudioshort}}) en el proceso de creación de Knowledge Graph, puede ayudar a crear gráficos de conocimiento específicos de dominios que se pueden aplicar en dominios como, por ejemplo, el financiero, el tecnológico, el de la seguridad, el de la inteligencia o el de la salud, entre muchos otros. 

Se han añadido dos nuevos puntos finales a {{site.data.keyword.discoveryfull}} – proporcionando la posibilidad de buscar entidades desambiguadas y relaciones enriquecidas a través de documentos en recopilaciones de documentos no estructurados. Los resultados de la búsqueda se pueden clasificar según su relevancia o popularidad. Además para una señal de búsqueda, las API pueden utilizar pasajes o palabras de contexto opcionales que encuentran relaciones y entidades más relevantes dentro del amplio gráfico de conocimiento creado de forma automática. 

 En la siguiente figura se muestra cómo Knowledge Graph se puede adecuar a su conducto actual de {{site.data.keyword.discoveryfull}}. {{site.data.keyword.nlushort}} enriquece los documentos con entidades y documentos a nivel de documento individual. Durante la creación de Knowledge Graph, se utilizan técnicas de expansión de gráficos y resolución implícitas automáticas de entidades a través de los documentos. Además del gráfico de conocimiento que se creará, el servicio de analíticas de Knowledge Graph añade técnicas de clasificación de rangos por relevancia a los resultados devueltos. 

![Proceso de Knowledge Graph ](images/knowledge-graph.png)

Este gráfico conectado de conocimientos y técnicas de clasificación proporciona: 

-  Entidades desambiguadas utilizando una señal de búsqueda difusa, información de tipo (opcional) y contexto (opcional). Ejemplo: Buscando `Steve` en el contexto de `Apple` se devuelve `Steve Jobs` al principio de la búsqueda, mientras que al buscar `Steve` en el contexto de `Microsoft` se devuelve `Steve Ballmer` en primer lugar. 
-  Relaciones clasificadas por su relevancia cuando se especifica una señal de búsqueda difusa y un contexto (opcional). La clasificación por relevancia utiliza las propiedades globales del gráfico para que aparezca información más específica. Ejemplo: Al buscar relaciones de `Obama` en el contexto de `health` devuelve `Affordable Care Act` y otras entidades relacionadas. 
-  Inferencias y agregaciones en los documentos mediante la realización de consultas de entidades y relaciones en un gráfico conectado de conocimiento. Algunos ejemplos de tales consultas son: ¿Cómo está la persona X relacionada con la persona Y? ¿Cuán diferente son los patrones de acceso a los datos del empleado X respecto a la norma? ¿Cuál es la esfera de influencia de la persona X?

## Requisitos del servicio

Durante el release beta, los métodos y funcionalidades asociados a Knowledge Graph solo estarán disponibles a instancias de servicio suscritas al plan **Advanced**. 

## Requisitos de recopilación

{{site.data.keyword.discoveryshort}} utiliza entidades y relaciones extraídas de documentos ingeridos para crear el Knowledge Graph y permitir consultas de entidades y relaciones. 

**Nota:** Knowledge Graph solo se puede utilizar en recopilaciones privadas, no ha sido diseñado para ser utilizado con {{site.data.keyword.discoverynewsshort}}. 

Para utilizar Knowledge Graph, la recopilación se debe configurar para satisfacer los siguientes requisitos específicos: 

-  Se deben especificar los enriquecimientos `entities` y `relations` para los campos que Knowledge Graph utilizará. Además, cada enriquecimiento debe utilizar el mismo modelo personalizado. Si se necesita el modelo público, se debe especificar en forma de un modelo personalizado `model="en-news"`.  

-  Los enriquecimientos `relations` se deben especificar de la siguiente manera: 
   ```json
   "relations": {
     "model": "en-news"
   }
   ```
   {: codeblock}

-  Se debe especificar el enriquecimiento `entities` y también se deben especificar los parámetros `mentions`, `mentions_types` y `sentence_locations`: 
   ```json
   "entities": {
     "mentions": true,
     "mention_types": true,
     "sentence_locations": true,
     "model": "en-news"
    }
    ```
    {: codeblock}

   Si se desea, se pueden especificar otras opciones opcionales de `enrichments` como, por ejemplo, `"sentiment": true`. 

Estas opciones no se pueden añadir utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, es necesario cargar una configuración personalizada utilizando la API. [Aquí](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json) encontrará disponible una copia de la configuración predeterminada modificada para enriquecer el campo `text` para que se pueda utilizar la recopilación con un gráfico de conocimiento con el modelo público. 

Cree una configuración personalizada como la siguiente, después de crear una instancia de servicio de {{site.data.keyword.discoveryshort}} :

1. Emita el siguiente mandato para crear un entorno denominado `my-first-environment`. Sustituya `{username}` y `{password}` con sus credenciales de servicio: 

   
```bash
   curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d '{ "name":"my-first-environment", "description":"exploring environments"}' "api/v1/environments?version=2017-11-07"
   ```
   {: pre}

   La API devuelve información como, por ejemplo, el ID de entorno, el estado del entorno y cuánto almacenamiento utiliza su entorno.

   Necesitará el `{environment_id}` que se devuelva.

1. A continuación, cree una configuración personalizada. Este procedimiento supone que está cargando el que se encuentra
[aquí](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/discovery/config-default-kg.json). Si desea crear su propia configuración personalizada, consulte la [referencia de configuración](/docs/services/discovery/custom-config.html).

   ```bash
   curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d config-default-kg.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
   ```
   {: pre}

1. Después de que se haya cargado la configuración personalizada, está puede ser utilizada en cualquier recopilación que haya creado y método para cargar documentos siempre que se especifique dicha configuración personalizada. Si no está familiarizado con la creación de recopilaciones y la carga de documentos, consulte [Iniciación al conjunto de herramientas](/docs/services/discovery/getting-started-tool.html). Cuando llegue al [paso 3](/docs/services/discovery/getting-started-tool.html#create-custom-configuration) seleccione `Configuración de Knowledge Graph` en lugar de crear una nueva configuración.

## Consultas de entidades
{: #entities}

En el release beta de Knowledge Graph, las consultas de entidades dan soporte a la desambiguación de entidades con base al contexto. Con base en el texto de entidad proporcionado y al texto de contexto opcional, la desambiguación identifica entidades únicas y devuelve una lista de entidades clasificadas con base a la información de contexto. Una consulta de entidades de Knowledge Graph se realiza con solicitudes `POST` a objetos `JSON` para el punto final `v1/environments/{environment_id}/collections/{collection_id}/query_entities`.

Se pueden consultar entidades con la API o con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Consulte [Consultas de Knowledge Graph utilizando el conjunto de herramientas de Discovery](/docs/services/discovery/building-kg.html#querying-kg) para obtener información sobre el conjunto de herramientas.

El objeto JSON de consulta de entidades de Knowledge Graph sigue el siguiente formato:

```json
{
  "feature": "disambiguate",
  "entity": {
    "text": "Steve",
    "type": "Person"
  },
  "context": {
    "text": "iphone"
  },
  "count": 10
}
```
{: codeblock}

-  `"feature": string` _obligatorio_ - la característica de consulta de entidad a utilizar debe ser `disambiguate`.
-  `"entity": {}` _obligatorio_ - un objeto que contiene información de la entidad a desambiguar.
   -  `"text": string` _obligatorio_ - el texto de la entidad que se desambiguará
   -  `"type": string` _opcional_ - el tipo de la entidad opcional que se utilizará para la desambiguación, si no se especifica, se incluyen todos los tipos.
-  `"context": {}` _opcional_ - un objeto opcional que incluye requisitos contextuales para la desambiguación.
   -  `"text": string` _opcional_ - Texto de entidad para proporcionar contexto para la clasificación y entidades consultadas basadas en dicha asociación. Por ejemplo, si desea consultar la ciudad de London en England, su consulta buscaría `London` con el contexto de `England`. La entrada puede corresponder a nombres parciales o pasajes extensos con términos de entidad relevantes. Se pueden pasar varios términos a la vez.
-  `"count": INT` _opcional_ - El número de entidades desambiguadas a devolver. El valor predeterminado es de `10`. El máximo es de `1000`

La consulta devuelve los resultados en el siguiente formato:

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON"
    },
    {
      "text": "Steve Wozniak",
      "type": "PERSON"
    }
  ]
}
```
{: codeblock}

Si no se encuentra ninguna coincidencia, se devuelve el siguiente objeto JSON:

```json
{
  "entities": []
}
```
{: codeblock}

## Consultas de relaciones
{: #relations}

Las consultas de relaciones de Knowledge Graph dan soporte a la búsqueda de las relaciones más relevantes con base a una entrada formada por entidades utilizando desambiguación de entidades implícita, relaciones basadas en el contexto, clasificación por puntuación de relevancia y recuento de menciones y por creación de filtros de ID de documento y tipos.

Se pueden consultar relaciones con la API o con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Consulte [Consultas de Knowledge Graph utilizando el conjunto de herramientas de Discovery](/docs/services/discovery/building-kg.html#querying-kg) para obtener información sobre el conjunto de herramientas.

Una consulta de entidades de Knowledge Graph se realiza con solicitudes `POST` a objetos `JSON` para el punto final `v1/environments/{environment_id}/collections/{collection_id}/query_relations`. El objeto JSON de consulta de relaciones de Knowledge Graph sigue el siguiente formato:

```json
{
  "entities": [
    {
      "text": "Steve Jobs",
      "type": "PERSON",
      "exact": true
    }
  ],
  "context": {
    "text": "iphone"
  },
  "sort": "score",
  "filter": {
    "relation_types": {
      "exclude": ["colocation"],
      "include": ["locatedAt", "employedBy", "managerOf", "founderOf"]
    },
    "entity_types": {
      "exclude": ["EVENT"],
      "include": ["PERSON", "GPE", "ORGANIZATION"]
    },
    "document_ids": ["b95df4c1-d00f-4771-abb2-a52baea0444a", "ad340635-bf3e-47a5-bea5-5e778f600c32"]
  },
  "count": 10
}
```
{: codeblock}

-  `"entities": []` _obligatorio_ - una matriz que contiene las entidades que consultarán las relaciones. Se devuelven todas las relaciones vecinas si solo se define un objeto de entidad. Cuando se define más de un objeto de entidad, se devuelven relaciones emparejadas mutuas. Las relaciones emparejadas mutuas devuelven las relaciones directas entre las entidades de entrada en lugar de las relaciones con todos los vecinos de entidad. Cada objeto de entidad contiene:
   -  `"text": string` _obligatorio_ - el texto de entidad.
   -  `"type": string` _opcional_ - el tipo de entidad opcional. Este campo es obligatorio si `"exact"` es `true`.
   -  `"exact": boolean` _opcional_ - Si es `false`, se realiza una desambiguación implícita. La desambiguación implícita utilizará la primera entidad desambiguada para cada objeto de entidad de entrada. El valor predeterminado es `false`.
-  `"context": {}` _opcional_ - un objeto opcional que incluye requisitos contextuales.
   -  `"text": string` _opcional_ - Texto de entidad para proporcionar contexto para la clasificación y entidades consultadas basadas en dicha asociación. Por ejemplo, si desea consultar la ciudad de London en England, su consulta buscaría `London` con el contexto de `England`. La entrada puede corresponder a nombres parciales o pasajes extensos con términos de entidad relevantes. Se pueden pasar varios términos a la vez.
-  `"sort": string` _opcional_ - método de clasificación para las relaciones. Puede ser `score` o `frequency`. El valor predeterminado es `score`. `score` se basa en la relevancia de las relaciones y los vecinos para la entidad de entrada y la relevancia para el contexto (si se proporciona uno). `frequency` es el número de veces únicas que se identifica cada relación.
-  `"filter": {}` _opcional_ - un objeto que contiene tipos de relación, tipos de entidad y documentos específicos por los que filtrar la consulta. De forma predeterminada, no se excluye nada.
   -  `"relation_types": {}` _opcional_ una lista de tipos de relación por los que filtrar.
      -  `"exclude": []` _opcional_ una lista separada por comas de tipos de relación a excluir de la consulta.
      -  `"include": []` _opcional_ una lista separada por comas de tipos de relación a incluir de forma explícita en la consulta. Si se especifica, se consideran excluidos todos los otros tipos.
   -  `"entity_types": {}` _opcional_ una lista de tipos de entidad para filtrar vecinos. No se aplica cuando la entrada contiene varias entidades porque no se devuelve ningún nuevo vecino.
      -  `"exclude": []` _opcional_ una lista separada por comas de tipos de entidad a excluir de la consulta.
      -  `"include": []` _opcional_ una lista separada por comas de tipos de entidad a incluir de forma explícita en la consulta. Si se especifica, se consideran excluidos todos los otros tipos.
   -  `"document_ids": []` _opcional_ una lista separada por comas de documentos en los que realizar la consulta de relaciones.
-  `"count": INT` _opcional_ El número de relaciones a devolver. El valor predeterminado es de `10`. El máximo es de `1000`.

La consulta devuelve los resultados en el siguiente formato:

```json
{
  "relations": [
    {
      "type": "FOUNDEROF",
      "frequency": 7,
      "arguments": [
        {
          "entities": [
            {
              "type": "PERSON",
              "text": "Steve Jobs"
            }
          ]
        },
        {
          "entities": [
            {
              "type": "ORGANIZATION",
              "text": "Apple"
            }
          ]
        }
      ]
    }
  ]
}
```
{: codeblock}

En cada objeto en la matriz de relaciones, se devuelve una matriz de argumentos con un par de matrices de entidades, la primera como origen o sujeto y la segunda como destino u objeto de la relación.

Si no se encuentra ninguna coincidencia, se devuelve el siguiente objeto JSON:

```json
{
  "relations": []
}
```
{: codeblock}

## Consultas de Knowledge Graph utilizando el conjunto de herramientas de Discovery
{: #querying-kg}

Aquellas con instancias de servicio suscritas al plan [**Avanzado**](/docs/services/discovery/building-kg.html#service-requirements) pueden consultar recopilaciones privadas con Knowledge Graph utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.

Para acceder a las consultas de Knowledge Graph en el conjunto de herramientas de {{site.data.keyword.discoveryshort}}:

1.  Pulse ![Icono consultar](images/search_icon.svg)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> para abrir la página de consultas.
1.  Seleccione su recopilación y pulse **Iniciación**.
1.  En la pantalla **Crear consultas**, elija el separador **Knowledge Graph** y, a continuación, **Entidades** o **Relaciones**.

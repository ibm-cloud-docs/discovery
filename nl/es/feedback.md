---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-17"

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

# Supervisión de uso
{: #usage}

Puede supervisar y realizar un seguimiento de la instancia de {{site.data.keyword.discoveryshort}} y utilizar estos datos para comprender y mejorar sus aplicaciones. Las [API de sucesos![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} pueden utilizarse para crear entradas de log que están asociadas a consultas y acciones de lenguaje natural específicas. Por ejemplo, puede registrar qué documentos de un conjunto de resultados ha "seleccionado" un usuario y cuándo lo ha hecho.

**Nota:** Los registros y sucesos solo se supervisan en consultas de lenguaje natural de recopilaciones de datos privadas. No se ha recopilado ningún registro en {{site.data.keyword.discoverynewsfull}}.

{{site.data.keyword.discoveryshort}} puede registrar la información siguiente:
- **Consultas** - Las consultas de lenguaje natural se ejecutan en recopilaciones de su entorno 
- **Impresiones** (o **Resultados**) - Los resultados devueltos de una consulta determinada, normalmente documentos o pasajes 
- **Sucesos** - Interacciones que realiza un usuario en un resultado o conjunto de resultados de {{site.data.keyword.discoveryshort}} (por ejemplo, una pulsación en el resultado de un documento)

Las **consultas** e **impresiones** se registran automáticamente; es posible integrar los **sucesos** que se registran en su aplicación mediante la API.

## Visualización de registros
{: #viewlogs}

Puede buscar la consulta y el registro de sucesos para buscar sesiones de consulta que coincidan con los criterios especificados. La búsqueda del punto final `logs` utiliza la sintaxis de consulta estándar de {{site.data.keyword.discoveryshort}} en los parámetros soportados. El punto final proporciona una funcionalidad de consulta básica para ver y buscar en los datos grabados.  

El punto final `/api/v1/logs` ofrece soporte a los parámetros de consulta de {{site.data.keyword.discoveryshort}} siguientes.
- query 
- filter
- sort
- count 
- offset
- version

Para obtener más detalles sobre la funciona y la sintaxis de los parámetros, consulte [Parámetros de consulta](/docs/services/discovery/query-parameters.html).

Ejemplo de registros de búsqueda de una consulta de lenguaje natural que contiene el término "train":

`https://gateway.watsonplatform.net/discovery/api/v1/logs?version=2018-03-28&query=train`

La respuesta de la consulta `logs` incluye resultados similares a los del documento de {{site.data.keyword.discoveryshort}}. Cada resultado será una consulta o un suceso, especificado en el campo `type` del documento.  

Ejemplo de registro de consulta:

```
{
            "customer_id": "",
            "environment_id": "252e6e82-c2d2-450e-9670-0008b0a3a99c",
            "natural_language_query": "how do i get from the airport to the city",
            "query_id": "_Qs35yOoa7",
            "document_results": {
                "count": 2,
                "results": [
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 6.724753491503856,
                        "position": 1,
                        "document_id": "4193eaa727d79b0f74597356dbcbb9a7"
                    },
                    {
                        "collection_id": "af9e1f41-6114-4d77-bca6-c9b99b2601b1",
                        "score": 5.791631414211986,
                        "position": 2,
                        "document_id": "bdcd6a9cc1438a3faa8c925f6a8d9429"
                    }
                ]
            },
            "event_type": "query",
            "session_token": "1_LKczxWGEWx5TJAi1_Qs35yOoa7",
            "created_timestamp": "2018-09-12T05:20:07.469Z"
        }
```

Con los registros de consulta puede investigar el tipo de resultados devueltos a los usuarios finales y buscar formas de mejorar la calidad de los resultados mediante los métodos disponibles en {{site.data.keyword.discoveryshort}}. Por ejemplo: 
- formación de relevancia, consulte [Mejora de la relevancia de los resultados con la API](/docs/services/discovery/train.html) y [Mejora de la relevancia de los resultados con el conjunto de herramientas](/docs/services/discovery/train-tooling.html)
- [operadores de consulta](/docs/services/discovery/query-operators.html)
- [expansión de la consulta](/docs/services/discovery/using.html#query-expansion)
- configuraciones personalizadas, consulte la [Referencia de configuración](/docs/services/discovery/custom-config.html)

## Creación de registros de sucesos
{: #eventlogs}

Los registros de sucesos se utilizan para realizar un seguimiento de las interacciones de los usuarios en su aplicación. Esto puede ayudarle a comprender el rendimiento de su aplicación, además de a identificar las áreas en las que necesita centrarse para mejorar los resultados. {{site.data.keyword.discoveryshort}} proporciona una API que se puede incorporar en la aplicación para realizar seguimientos de sucesos. Al llamar esta API con la información adecuada cuando un usuario lleva a cabo una acción, se devuelve una señal a {{site.data.keyword.discoveryshort}} que podrá visualizarse en los registros. 

Los sucesos pueden ayudar a recopilar información sobre métricas de cálculo (como la tasa de clics) para medir la efectividad de la aplicación al ayudar a los usuarios finales a buscar información relevante, o puede utilizarse para ayudar a mejorar la formación revisando las consultas y clics para empezar a crear la verdad terreno. 

Puede añadir esta API siempre que los usuarios interactúen con los resultados. Por ejemplo, en una IU de búsqueda puede que desee añadirla cuando un usuario pulse en un enlace de documento, o en una interfaz de chatbot puede que desee utilizarla para realizar un seguimiento a un usuario cuando pulse en el botón **Expandir** o **Más detalles**.

Los resultados de {{site.data.keyword.discoveryshort}} devolverán información adicional que se puede utilizar para realizar un seguimiento de sucesos, incluida la señal de sesión. 

`"matching_results": 179,`
`"session_token": "1_LKczxWGEWx59fYD0_VV8HFUpb6"`

Para registrar un suceso, realice una POST en el punto final `/api/v1/events`. Consulte [API de sucesos![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#events-and-feedback-api){: new_window} para obtener más detalles.

Una vez se haya registrado un suceso, se puede leer de nuevo mediante el punto final `/api/v1/logs`. Unir sucesos a la consulta asociada utilizando `session_token`.

---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-03"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Sugerencias de entrenamiento de relevancia
{: #relevancy-tips}

 Aquí se pretende responder a preguntas habituales sobre el entrenamiento de una recopilación y las explicaciones de los errores y mensajes de aviso más habituales. Para obtener más información sobre cómo mejorar la relevancia de las consultas en lenguaje natural, consulte [Mejora de la relevancia de los resultados con el conjunto de herramientas](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#improving-result-relevance-with-the-tooling) y [Mejora de la relevancia de los resultados con la API](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#improving-result-relevance-with-the-api).
{: shortdesc}

## Información sobre el entrenamiento
{: #understanding-training}

Aquí se pretende responder a preguntas habituales sobre el entrenamiento de una recopilación.

### ¿Cómo sé si mi sistema está entrenado?
{: #understanding-system}

Utilice el mandato de API [Listar detalles de recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#get-collection-details){: new_window} para verificar si se ha entrenado el sistema.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

Respuesta de ejemplo:

```json
{
  "training_status": {
    "data_updated": "2017-02-10T14:18:22.786Z",
    "total_examples": 54,
    "sufficient_label_diversity": false,
    "processing": false,
    "minimum_examples_added": true,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "available": true,
    "notices": 13,
    "minimum_queries_added": true    
    }
}
```

Para satisfacer las necesidades de entrenamiento, todos estos parámetros deben ser `true`:
- `minimum_queries_added`
- `minimum_examples_added`
- `sufficient_label_diversity`   

En la respuesta:
- `successfully_trained` corresponde a la última hora en la que el entrenamiento se completó de forma satisfactoria.
- `available: true` indica que el entrenamiento realizado en un modelo está disponible.
- `processing: true` indica que el entrenamiento está en curso.
-  Si la fecha `data_updated` es posterior a la fecha `successfully_trained`, un nuevo modelo no se ha entrenado puesto que recientemente se ha realizado una carga de datos.  

### ¿Cómo puedo comprobar errores y avisos?
{: #understanding-errors}

Utilice [API consultar avisos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#query-system-notices){: new_window} para ver los errores y/o avisos.  

```bash
curl -u "apikey":"{apikey_value}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

En [Realización de otras operaciones de consultas de datos de entrenamiento](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-api#training-data-operations) encontrará listadas otras operaciones de API.

### ¿Cómo interpretar la puntuación de `confidence` que aparece en los resultados de las consultas en lenguaje natural después del entrenamiento?
{: #interpret-confidence}

Consulte [Puntuaciones de confianza](/docs/services/discovery?topic=discovery-improving-result-relevance-with-the-tooling#confidence) para obtener más información.  

## Interpretación de errores y avisos
{: #interpreting-errors}

Explicaciones de los mensajes de error y avisos más habituales.

### Aviso: `Se han encontrado datos de entrenamiento no válidos: El documento no se ha devuelto en los primeros 100 resultados de búsqueda para la entrada dada, y por lo tanto, no se utilizará para el entrenamiento`
{: #warning-docnotreturned}

Este aviso lo originan `document_ids` en los datos de entrenamiento que no coinciden con los `document_ids` en una búsqueda realizada en la recopilación. Debe comprobar las consultas y asegurarse de que el `document_id` del documento que está valorado se devuelve en los primeros 100 resultados para dicha consulta. Si no es así, podría comprobar dos cosas:  

- Si el documento no se devuelve en los primeros 100 resultados, podría deberse a que no es un buen ejemplo de un resultado de alta calidad. Debería revisar la razón por la que se eligió este documento.  

- Si el documento no se devuelve en absoluto, debería revisar la razón por la que no se devuelve y ver si hay algún texto en el documento que realmente coincide con partes de la consulta.  

**Nota:** Este aviso indica que podría tener una o varias consultas incorrectas; no es una indicación que no se haya realizado el entrenamiento.  

### Error: `Se han encontrado datos de entrenamiento no válidos: Error de sintaxis al analizar la consulta.`
{: #error-syntax}

- Esto significa que hay un problema con la sintaxis de la consulta real. Compruebe que la consulta devuelva resultados y de que no presenta un error de sintaxis. Esto sólo puede ocurrir si ha añadido un filtro a su consulta de lenguaje natural.

### Error: `Se han encontrado datos de entrenamiento no válidos: La serie de la consulta que ha proporcionado excede la longitud máxima, proporcione una más corta`
{: #error-exceedlength}

- La longitud máxima de la serie de consulta es `2048`. Deberá acortar la consulta específica. Incluir un filtro en la consulta es una manera de evitarlo.  

### Error: `No es posible entrenar esta recopilación: Su plan no da soporte al entrenamiento a este número de campos de texto de nivel superior.`
{: #error-toplevelfields}

- Este error sólo se produce con los planes `Lite`. Los campos de nivel superior son aquellos campos que no están anidados bajo otro campo. El aprendizaje solo se realiza en los campos de nivel superior y, por lo tanto, hay límites en lo que se refiere al número de campos que se pueden utilizar en el proceso de entrenamiento. Cuantos más campos de nivel superior hay en una colección, son necesarios más datos de entrenamiento. Además, es más probable que el entrenamiento encuentre errores en los casos en los que haya más de `10` campos de nivel superior. 

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: Necesitará consultas de entrenamiento adicionales con ejemplos etiquetados. (Para ser considerados para el entrenamiento, cada ejemplo debe aparecer en los primeros 100 resultados de su consulta).`
{: #error-labels}

- Esto significa que necesita añadir más datos de entrenamiento para poder completarlo de forma satisfactoria. Necesita al menos 49 consultas de entrenamiento únicas como mínimo, y cada una necesita al menos un documento valorado. Mínimo no significa óptimo. El tamaño de la recopilación, así como otros factores, pueden incrementar el número mínimo de ejemplos de entrenamiento necesarios.  

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: Número insuficiente de consultas de entrenamiento únicas. Se esperaban como mínimo n, pero se han encontrado m.`
{: #error-notunique}

- Para poder satisfacer los requisitos de entrenamiento mínimos, necesita al menos 49 consultas de entrenamiento únicas como mínimo, y cada una necesita al menos un documento clasificado. Si tiene más y todavía sigue recibiendo este mensaje de error, debería comprobar los avisos para encontrar otros errores.  

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: No se han encontrado documentos con etiquetas de relevancia no nulas.`
{: #error-relevance}

- Los datos de entrenamientos precisan de suficientes datos etiquetados que especifican los documentos de valor elevado. Esto significa que debe valorar algunos documentos con valores no nulos. Si está utilizando el conjunto de herramientas de Discovery, necesitará valorar algunos documentos como Relevantes (`10`). Si utiliza la API, necesitará etiquetar algunos documentos como `1` o por encima.   

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: Los ejemplos de entrenamiento no tienen una variedad de etiqueta de relevancia para X consultas.`
{: #error-variety}

- Uno de los requisitos del entrenamiento es tener suficiente diversidad en las etiquetas. Esto significa que si desea conseguir un sistema bien entrenado, debería añadir no únicamente documentos con la mayor relevancia, sino también documentos con una "buena" relevancia. En otras palabras, si tiene una escala del 0 al 4, ayuda tener documentos valorados como 2 y 3 además de aquellos valorados con 4. (Si está utilizando el conjunto de herramientas de Discovery, los documentos se valoran como Relevantes (`10`) o No relevantes (`0`)). Al menos el 25% de las preguntas deben presentar alguna variedad de etiqueta.   

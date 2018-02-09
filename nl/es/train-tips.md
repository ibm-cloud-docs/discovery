---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-14"

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

# Sugerencias de entrenamiento de relevancia
{: #relevancy-tips}

 Aquí se pretende responder a preguntas habituales sobre el entrenamiento de una recopilación y las explicaciones de los errores y mensajes de aviso más habituales. Para obtener más información sobre cómo mejorar la relevancia de las consultas en lenguaje natural, consulte [Mejora de la relevancia de los resultados con el conjunto de herramientas](/docs/services/discovery/train-tooling.html) y [Mejora de la relevancia de los resultados con la API](/docs/services/discovery/train.html).
{: shortdesc}

## Información sobre el entrenamiento

Aquí se pretende responder a preguntas habituales sobre el entrenamiento de una recopilación. 

### ¿Cómo sé si mi sistema está entrenado?

Utilice el mandato de API [Listar detalles de recopilación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/?curl#list-collection-details){: new_window} para verificar si se ha entrenado el sistema.   

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}?version=2017-11-07"
```
{: pre}

Respuesta de ejemplo:

```json
{
  "training": {
    "total_examples": 54,
    "available": true,
    "processing": false,
    "minimum_queries_added": true,
    "minimum_examples_added": true,
    "sufficient_label_diversity": false,
    "notices": 13,
    "successfully_trained": "2017-02-08T14:18:22.786Z",
    "data_updated": "2017-02-10T14:18:22.786Z"
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

Utilice [API consultar avisos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/watson/developercloud/discovery/api/v1/#query-notices){: new_window} para ver los errores y/o avisos.   

```bash
curl -u "{username}":"{password}" https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/notices?version=2017-11-07"
```
{: pre}

En [Realización de otras operaciones de consultas de datos de entrenamiento](/docs/services/discovery/train.html#training-data-operations) encontrará listadas otras operaciones de API. 

### ¿Cómo interpretar la puntuación de `confidence` que aparece en los resultados de las consultas en lenguaje natural después del entrenamiento? 

Las recopilaciones entrenadas devolverán una puntuación de `confidence` en el resultado de una consulta de lenguaje natural. Este valor de `confidence` se calcula con base a la relevancia de un resultado en comparación con el modelo entrenado. La puntuación de `confidence` **no** es la misma que la de `score`. Consulte [Puntuaciones de confianza](/docs/services/discovery/train-tooling.html#confidence) para obtener más información.   

## Interpretación de errores y avisos

Explicaciones de los mensajes de error y avisos más habituales. 

### Aviso: `Se han encontrado datos de entrenamiento no válidos: El documento no se ha devuelto en los primeros 100 resultados de búsqueda para la entrada dada, y por lo tanto, no se utilizará para el entrenamiento`

Este aviso lo originan `document_ids` en los datos de entrenamiento que no coinciden con los `document_ids` en una búsqueda realizada en la recopilación. Debe comprobar las consultas y asegurarse de que el `document_id` del documento que está valorado se devuelve en los primeros 100 resultados para dicha consulta. Si no es así, podría comprobar dos cosas:   

- Si el documento no se devuelve en los primeros 100 resultados, podría deberse a que no es un buen ejemplo de un resultado de alta calidad. Debería revisar la razón por la que se eligió este documento.   

- Si el documento no se devuelve en absoluto, debería revisar la razón por la que no se devuelve y ver si hay algún texto en el documento que realmente coincide con partes de la consulta.   

**Nota:** Este aviso indica que podría tener una o varias consultas incorrectas; no es una indicación que no se haya realizado el entrenamiento.   

### Error: `Se han encontrado datos de entrenamiento no válidos: Error de sintaxis al analizar la consulta. `

- Esto significa que hay un problema con la sintaxis de la consulta real. Compruebe que la consulta devuelva resultados y de que no presenta un error de sintaxis. Esto sólo puede ocurrir si ha añadido un filtro a su consulta de lenguaje natural. 

### Error: `Se han encontrado datos de entrenamiento no válidos: La serie de la consulta que ha proporcionado excede la longitud máxima, proporcione una más corta`

- La longitud máxima de la serie de consulta es `X`. Deberá reducir la consulta específica. Incluir un filtro en la consulta es una manera de evitarlo.   

### Error: `No es posible entrenar esta recopilación: Su plan no da soporte al entrenamiento a este número de campos de texto de nivel superior. `

- Este error sólo se produce con los planes `Lite`. El número máximo de campos de texto de nivel superior por los que se puede entrenar es de `X`. Los campos de nivel superior son aquellos campos que no están anidados bajo otro campo. El aprendizaje solo se realiza en los campos de nivel superior y, por lo tanto, hay límites en lo que se refiere al número de campos que se pueden utilizar en el proceso de entrenamiento.   

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: Necesitará consultas de entrenamiento adicionales con ejemplos etiquetados. (Para ser considerados para el entrenamiento, cada ejemplo debe aparecer en los primeros 100 resultados de su consulta). `

- Esto significa que necesita añadir más datos de entrenamiento para poder completarlo de forma satisfactoria. Necesita al menos 49 consultas de entrenamiento únicas como mínimo, y cada una necesita al menos un documento valorado. Mínimo no significa óptimo. El tamaño de la recopilación, así como otros factores, pueden incrementar el número mínimo de ejemplos de entrenamiento necesarios.   

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: Número insuficiente de consultas de entrenamiento únicas. Se esperaban como mínimo n, pero se han encontrado m.`

- Para poder satisfacer los requisitos de entrenamiento mínimos, necesita al menos 49 consultas de entrenamiento únicas como mínimo, y cada una necesita al menos un documento clasificado. Si tiene más y todavía sigue recibiendo este mensaje de error, debería comprobar los avisos para encontrar otros errores.   

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: No se han encontrado documentos con etiquetas de relevancia no nulas.` 

- Los datos de entrenamientos precisan de suficientes datos etiquetados que especifican los documentos de valor elevado. Esto significa que debe valorar algunos documentos con valores no nulos. Si está utilizando el conjunto de herramientas de Discovery, necesitará valorar algunos documentos como Relevantes (`10`). Si utiliza la API, necesitará etiquetar algunos documentos como `1` o por encima.    

### Error: `No se cumplen los estándares de calidad de los datos de entrenamiento: Los ejemplos de entrenamiento no tienen una variedad de etiqueta de relevancia para X consultas. ` 

- Uno de los requisitos del entrenamiento es tener suficiente diversidad en las etiquetas. Esto significa que si desea conseguir un sistema bien entrenado, debería añadir no únicamente documentos con la mayor relevancia, sino también documentos con una "buena" relevancia. En otras palabras, si tiene una escala del 0 al 4, ayuda tener documentos valorados como 2 y 3 además de aquellos valorados con 4. (Si está utilizando el conjunto de herramientas de Discovery, los documentos se valoran como Relevantes (`10`) o No relevantes (`0`)). Al menos el 25% de las preguntas deben presentar alguna variedad de etiqueta.    

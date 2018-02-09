---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-05"

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

# Mejora de la relevancia de los resultados con el conjunto de herramientas

Las consultas de lenguaje natural se pueden mejorar en el servicio {{site.data.keyword.discoveryfull}} con el entrenamiento. Puede entrenar sus recopilaciones privadas con el conjunto de herramientas de {{site.data.keyword.discoveryshort}} o con las API de {{site.data.keyword.discoveryshort}}. Consulte [Mejora de la relevancia de los resultados de las consultas con la API](/docs/services/discovery/train.html) si prefiere utilizar las API.
{: shortdesc}

El entrenamiento de relevancia es opcional; si los resultados de sus consultas satisfacen sus necesidades, no es necesario un entrenamiento adicional. Para obtener una visión general de situaciones adecuadas para el entrenamiento, consulte el artículo de blog [Cómo sacar el mayor partido al entrenamiento de relevancia ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/dwblog/2017/get-relevancy-training/){: new_window}. 

Para entrenar Watson, necesitará: 

  -   Proporcionar consultas de ejemplo que sean representativas de las consultas de los usuarios y 
  -   Proporcionar valoraciones para indicar la relevancia de los resultados de cada consulta

Una vez Watson tenga suficientes datos de entrenamiento, la información que haya proporcionado sobre qué resultados son buenos y qué resultados son malos para cada consulta se utilizará para aprender sobre su recopilación. Watson no tan solo memoriza, aprende sobre la información específica de consultas individuales y aplica los patrones que detecta a todas las nuevas consultas. Este mecanismo se basa en las técnicas de Watson de aprendizaje máquina que encuentran señales en sus preguntas y el contenido. Una vez aplicado el entrenamiento, {{site.data.keyword.discoveryshort}} reordena los resultados de las consultas para visualizar en primer lugar los resultados más relevantes. A medida que se añaden más datos de entrenamiento, {{site.data.keyword.discoveryshort}} debería ser más preciso a la hora de ordenar los resultados de las consultas. 

El entrenamiento debe satisfacer los siguientes requisitos **mínimos** para que {{site.data.keyword.discoveryshort}} empiece a aplicar sus valoraciones: 

  - Debe entrenar un mínimo de 49 consultas, y posiblemente más. Watson le informará si son necesarias más consultas para el entrenamiento. 
  - Debería utilizar tanto valoraciones `relevantes` como `no relevantes`. Si únicamente valora documentos `relevantes` no estará proporcionando los datos necesarios. 

**Nota:** El entrenamiento de relevancia necesita determinados requisitos de datos de entrenamiento antes de ser efectivo. El servicio comprueba los datos de entrenamiento de forma periódica para determinar si se satisfacen estos requisitos, y se actualiza a sí mismo de forma automática con base a los cambios. 

**Nota:** El entrenamiento de relevancia solo se aplica a las consultas de lenguaje natural en recopilaciones privadas. No está pensado para ser utilizado con consultas estructuradas de {{site.data.keyword.discoveryshort}} Query Language. Para obtener más información sobre {{site.data.keyword.discoveryshort}} Query Language, consulte [Conceptos de consultas](/docs/services/discovery/using.html). 

**Nota:** Hay un máximo de 4 recopilaciones entrenadas por entorno.  

## Adición de consultas y valoración de la relevancia de los resultados

El entrenamiento consta de tres partes: una consulta de lenguaje natural, los resultados de la consulta y la valoración que asignará a dichos resultados. 

1.  En el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, puede acceder a la página de entrenamiento para una recopilación desde la pantalla **Crear consultas**. Pulse **Entrenar Watson para mejorar los resultados** en la parte superior derecha. No es necesario especificar una consulta en la pantalla **Crear consulta** para iniciar el entrenamiento. 
1.  En la pantalla **Entrenar Watson**, pulse **Añadir una consulta de lenguaje natural** como, por ejemplo: "IBM Watson in healthcare" y, a continuación, añádala. Asegúrese de escribir la consulta tal como lo harían sus usuarios. Además, las consultas de entrenamiento se deberían escribir con alguna superposición de términos entre la consulta y la respuesta deseada. Esto mejorará los resultados iniciales al ejecutar la consulta de lenguaje natural. El entrenamiento de relevancia solo utiliza consultas de lenguaje natural, no especifique consultas escritas en {{site.data.keyword.discoveryshort}} Query Language.
1.  Para ver los resultados de la consulta, pulse el botón **Valorar resultados** junto a los resultados. Si piensa que no hay suficientes resultados, podría intentar rescribir la consulta, o añadir más documentos a esta recopilación a través de la pantalla **Gestionar datos**. 
1.  Empiece a valorar sus resultados como `relevantes` o `no relevantes`. Cuando haya terminado, pulse **Volver a las consultas**. En el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, `Relevante` tiene una puntuación de `10` y `No relevante` tiene una puntuación de `0`. Si ya ha empezado a valorar resultados para esta recopilación utilizando la API y utilizó una escala de puntuación diferente, se visualizará un mensaje de aviso, con opciones para corregir el problema. En la parte superior de la ventana, Watson realiza un seguimiento del estado del entrenamiento, y proporcionar consejos sobre lo que puede hacer para mejorar los resultados. "Añadir más variedad a sus valoraciones" significa que debería utilizar tanto valoraciones `relevantes` como `no relevantes`. Una vez que haya satisfecho los requisitos, el entrenamiento empezará a actualizarse de forma periódica. Le tomará menos de 30 minutos completarlo una vez haya empezado, luego podrá continuar trabajando a medida que Watson actualiza. 
1.  Continúe añadiendo consultas y valorando resultados. 

Para volver a la pantalla principal de **Crear consultas**, pulse **Crear consultas** en la parte superior derecha.
{: tip}
Para volver a la pantalla **Gestionar datos**, pulse sobre el nombre de la recopilación en la parte superior derecha.
{: tip}

Si desea suprimir todos los datos de entrenamiento en su recopilación al mismo tiempo, debe hacerlo a través de la API. Consulte [Supresión de todos los datos de entrenamiento de una recopilación](http://www.ibm.com/watson/developercloud/discovery/api/v1/#delete-all-training-data) para obtener más información. Para obtener más información sobre el entrenamiento a través de la API, consulte [Mejora de la relevancia de los resultados de las consultas con la API](/docs/services/discovery/train.html). 

## Realización de pruebas e iteración para la relevancia de resultados

Después de haber completado los resultados de valoración y de que Watson haya aplicado el entrenamiento, debe comprobar si los resultados de las consultas han mejorado. Para ello, ejecute consultas de prueba relacionadas (pero no idénticas) con las consultas de entrenamiento. Compruebe si los resultados de las consultas de prueba han mejorado. 

Si desea mejorar aún más los resultados después de las pruebas, puede:
- Añadir más documentos a la recopilación. 
- Añadir más consultas de entrenamiento. 
- Valorar más resultados, asegurándose de utilizar tanto las valoraciones `relevante` como `no relevante`. 

Consulte [Sugerencias de entrenamiento de relevancia](/docs/services/discovery/train-tips.html#relevancy-tips) para obtener más ayuda con relación al entrenamiento. 

## Puntuaciones de confianza
{: #confidence}

Las recopilaciones entrenadas devolverán una puntuación de `confidence` en el resultado de una consulta de lenguaje natural. Este valor de `confidence` se calcula con base a cómo se estima de relevante un resultado en comparación con el modelo entrenado. La puntuación de `confidence` **no** es la misma que la de `score`. Para obtener más información sobre la determinación de puntuaciones de confianza, consulte [
Cómo seleccionar un umbral para actuar utilizando puntuaciones de confianza ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/watson/blog/2016/06/23/how-to-select-a-threshold-for-acting-using-confidence-scores/). El valor de score no se debería utilizar para establecer umbrales absolutos puesto que es un cálculo relativo. 

El valor de `confidence` varía entre 0.0 y 1.0. Cuanto mayor es el número, mayor es la relevancia del documento. 

La puntuación de `confidence` se puede encontrar en los resultados de la consulta, bajo `result_metadata` en cada documento, por ejemplo: 

```json
    "results": [
        {
            "id": "eea16dfd5fe6139a25324e7481a32f89_13",
            "result_metadata": {
                "confidence": 0.5893963975910735,
                "score": 0.5006834
            },
```

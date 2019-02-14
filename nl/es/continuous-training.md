---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-25"

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

# Entrenamiento de relevancia continuo
{: #crt}

El entrenamiento de relevancia continuo de {{site.data.keyword.discoveryshort}} puede aprender del comportamiento del usuario de forma automática, lo que reduce significativamente el esfuerzo necesario para mejorar la clasificación de resultados de relevancia. Utiliza interacciones de usuarios para aprender a emerger los resultados más relevantes. Puede aprender de interacciones como los clics para determinar qué resultados son los más valiosos para los usuarios y descubrir las señales más importantes para consultas futuras. El entrenamiento de relevancia continuo volverá a clasificar los documentos para que aparezca la información más relevante en la parte superior de los resultados. Se puede utilizar para:

- Ayudar a mejorar la relevancia de los resultados de los agentes de soporte en función de los resultados en los que pulsan
- Mostrar resultados más relevantes en un chatbot del cliente en función de los resultados seleccionados a largo plazo 
- Proporciona expertos con respuestas más relevantes en función de los resultados que exploren

Para configurar el entrenamiento de relevancia continuo:

- El entrenamiento de relevancia continuo solo se puede habilitar a nivel de entorno. Las consultas deben utilizar los puntos finales `/api/v1/environment/{environment_id}/query` y `/api/v1/environments/{environment_id}/query` para consultar una o varias recopilaciones.
- Puesto que los `sucesos` (clics) de {{site.data.keyword.discoveryshort}} se utilizan para crear los datos de entrenamiento necesarios, integre primero el seguimiento de sucesos. Consulte [Supervisión de uso](/docs/services/discovery/feedback.html#usage) para obtener detalles.
- Se necesita un mínimo de 1000 consultas de lenguaje natural con un suceso pulsar para que se inicie el entrenamiento de relevancia continuo. Los sucesos y registros se conservan durante 30 días en la instancia, por lo que es necesario recopilar los 1000 clics durante dicho período de tiempo.
- El entrenamiento de relevancia continuo está disponible para los planes Avanzado de tamaño `Pequeño` o superior y los planes Premium. No está disponible para los planes `Lite`.
- El límite del número de recopilaciones del entrenamiento de relevancia continuo es `5`. Puesto que el entrenamiento de relevancia continuo funciona en varias recopilaciones, es posible expandir los tiempos de entrenamiento y consulta.
- El entrenamiento de relevancia continuo solo se realiza en los campos de nivel superior y, por lo tanto, hay límites en lo que se refiere al número de campos que se pueden utilizar en el proceso de entrenamiento. Es más probable que el entrenamiento encuentre errores en los casos en los que haya más de `10` campos de nivel superior. 

Para utilizar el entrenamiento de relevancia continuo:

Una vez que se haya entrenado, el entrenamiento de relevancia continuo se utiliza para influir en los resultados de `natural_language_query` al utilizar una consulta a nivel de entorno. 

El entrenamiento de relevancia continuo puede utilizarse en el momento de la consulta ejecutando la consulta `natural_language_query` de varias recopilaciones en todas las recopilaciones del entorno. Consulte [Consulta a varias recopilaciones](/docs/services/discovery/using.html#multiple-collections) para obtener instrucciones. 

**Nota:** El entrenamiento de relevancia continuo no afecta a las consultas realizadas en una llamada de consulta a nivel de recopilación entrenada o no entrenada (`/v1/environments/{environment_id}/collections/{collection_id}/query`). 

Estado del seguimiento:

El estado del entrenamiento de relevancia continuo se puede visualizar en el punto final de `/api/v1/environments`. Consulte la [referencia de API![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/curl.html?curl#environments-api){: new_window}. `status` proporcionará información sobre el estado de las operaciones de entrenamiento y le notificará si el entrenamiento de relevancia continuo está activo:

```
"search_status" : [
        {
            "scope" : "environment",
            "status" : "NO_DATA",
            "status_description" : "Discovery is employing a default strategy for document search natural_language_query. Enable query and event logging so we can initiate relevancy training to improve search accuracy.”
        }
    ]
```

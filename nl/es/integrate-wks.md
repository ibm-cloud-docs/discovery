---

copyright:
  years: 2015, 2018, 2019
lastupdated: "2019-01-08"

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

# Integración con Watson Knowledge Studio
{: #integrating-with-wks}

Puede integrar uno o varios modelos personalizados de {{site.data.keyword.knowledgestudiofull}} con el servicio {{site.data.keyword.discoveryshort}} para proporcionar enriquecimientos personalizados de relaciones y entidades.
{: shortdesc}

Esto ofrece la flexibilidad de aplicar las funcionalidades de mejora de documentos del servicio {{site.data.keyword.discoveryshort}} con información específica de áreas de un tema concreto como, por ejemplo, una disciplina concreta científica o de la industria. Se pueden utilizar tanto datos públicos como sus propios datos privados en el modelo de enriquecimiento.

Puede utilizar la API del servicio o el conjunto de herramientas de {{site.data.keyword.discoveryshort}} para integrar un modelo de {{site.data.keyword.knowledgestudioshort}} con el servicio de {{site.data.keyword.discoveryshort}}.

## Antes de empezar
{: #wks-beforeintegration}

Antes de poder integrar un modelo personalizado de {{site.data.keyword.knowledgestudioshort}} con el servicio {{site.data.keyword.discoveryshort}}, debe crear y desplegar el modelo utilizando {{site.data.keyword.knowledgestudioshort}}. Consulte la [Documentación de {{site.data.keyword.knowledgestudioshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window} para obtener información sobre cómo crear y desplegar modelos. Necesitará un ID exclusivo del modelo desplegado para integrarlo con el servicio {{site.data.keyword.discoveryshort}}.

## Integración de su modelo personalizado con la API
{: #integrate-customAPI}

1.  Obtenga el ID de su entorno de {{site.data.keyword.discoveryshort}} tal como se describe en [Listar entornos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#list_environments){: new_window}. Anote el ID de entorno.
1.  Liste los ID de su configuración o configuraciones de {{site.data.keyword.discoveryshort}} tal como se describe en [Listar configuraciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/discovery#list_configurations){: new_window} Anote el ID de configuración que desea integrar con su modelo personalizado de {{site.data.keyword.knowledgestudiofull}}.
1.  Descargue una copia de su configuración de {{site.data.keyword.discoveryshort}} actual ejecutando los siguientes mandatos en un shell bash o similar como, por ejemplo Cygwin para Windows. Sustituya `{environment_id}` y `{configuration_id}` con los ID que anotó en los dos pasos anteriores.

    ```bash
    curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
    ```
    {: pre}

    Este mandato muestra el contenido del archivo de configuración y lo coloca en un archivo JSON denominado `my_config.json`.
1.  Abra el archivo `my_config.json` en un editor de texto y realice los cambios siguientes:
    1.  Cambie el valor del campo `"name"` con un texto que indique el propósito de la nueva configuración. También puede cambiar opcionalmente el valor del campo `"description"`.

        ```json
        ...
        "name": "wks-config",
        "description": "This is a configuration to use with a WKS model",
        ...
        ```
        {: codeblock}

    1.  Actualice los campos de enriquecimiento con la información del modelo de {{site.data.keyword.knowledgestudioshort}}. Suponiendo que los campos de enriquecimiento originalmente indicasen:

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {}
                }
            }
        }]
        ```
        {: codeblock}

    1.  Actualizaríamos el archivo tal como se indica a continuación, sustituyendo el ID exclusivo del modelo de {{site.data.keyword.knowledgestudioshort}} descrito en "Antes de empezar" por el `{watson_knowledge_studio_model_ID}`.

        Se puede aplicar más de un modelo personalizado a campos idénticos utilizando la API. Consulte el ejemplo en [Integración de varios modelos personalizados](/docs/services/discovery?topic=discovery-integrating-with-wks#integrate-multiplecustom). Si también va a incorporar [Watson {{site.data.keyword.discoveryshort}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg), debe utilizar el mismo modelo para enriquecer tanto las entidades como las relaciones en un único objeto de enriquecimiento.
        {: note}

        ```json
        "enrichments": [
        {
            "source_field": "text",
            "destination_field": "enriched_text",
            "enrichment": "natural_language_understanding",
            "options": {
                "features": {
                    "entities": {
                        "sentiment": true,
                        "emotion": false,
                        "limit": 50,
                        "model": "{watson_knowledge_studio_model_ID}"
                    },
                    "sentiment": {
                        "document": true
                    },
                    "categories": {},
                    "concepts": {
                        "limit": 8
                    },
                    "relations": {
                        "model": "{watson_knowledge_studio_model_ID}"
                    }
                }
            }
        }]
        ```
        {: codeblock}

1.  Guarde el archivo `my_config.json`.
1.  Utilice un validador JSON como, por ejemplo [JSLint ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://jslint.com){: new_window} para validarlo y, si es necesario, corrija el JSON editado antes de realizar el siguiente paso.
1.  Actualice la configuración tal como se indica a continuación. De nuevo necesitará los ID de `{environment_id}` y `{configuration_id}` que recopiló al inicio de este procedimiento.

    ```bash
    curl -X PUT -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **Nota:** Si está creando una nueva configuración, o modificando la configuración predeterminada, deberá crear una nueva configuración personalizada en lugar de actualizar una configuración existente. Antes de crear una nueva configuración, asegúrese de que el campo `"configuration_id":` se elimina del archivo `my_config.json` y luego vuelva a ejecutar el siguiente mandato:

    ```bash
    curl -X POST -u "apikey":"{apikey_value}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    Ambos mandatos devuelven el contenido del archivo de configuración actualizado.

### Integración de varios modelos personalizados 
{: #integrate-multiplecustom}

Puede aplicar más de un modelo personalizado a campos idénticos utilizando la API. Siga los pasos de [Integración de su modelo personalizado con la API](/docs/services/discovery?topic=discovery-integrating-with-wks#integrate-customAPI) y utilice este ejemplo como guía. Si también va a incorporar [Watson {{site.data.keyword.discoveryshort}} Knowledge Graph](/docs/services/discovery?topic=discovery-kg#kg), debe utilizar el mismo modelo para enriquecer tanto las entidades como las relaciones en un único objeto de enriquecimiento. Consulte el ejemplo de `"destination_field": "enriched_text"` como guía.

No puede aplicar varios modelos personalizados utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Solo se pueden personalizar los enriquecimientos de relaciones y entidades.

Debe especificar un `destination_field` diferente para cada `source_field` idéntico. Además, cada `source_field` debe estar enriquecido por un modelo único. Por ejemplo, si desea aplicar varios modelos personalizados al `source_field` de `text` y aplica el `model` `{watson_knowledge_studio_model_ID}` al enriquecimiento `entities`, no debe utilizar dicho modelo de nuevo para el enriquecimiento `entities`.
{: tip}


```json
   "enrichments": [
   {
        "source_field": "text",
        "destination_field": "enriched_text",
        "enrichment": "natural_language_understanding",
        "options": {
            "features": {
                "entities": {
                    "model": "{watson_knowledge_studio_model_ID}"
                },
                "relations": {
                    "model": "{watson_knowledge_studio_model_ID}"
            }
        }
    }
},
   {
        "source_field": "text",
        "destination_field": "enriched_text_2",
        "enrichment": "natural_language_understanding",
        "options": {
            "features": {
                "entities": {
                    "model": "{watson_knowledge_studio_model_ID_b}"
            },
                "relations": {
                    "model": "{watson_knowledge_studio_model_ID_c}"
            }
        }
    }
}]
```
{: codeblock}    

## Integración de su modelo personalizado con el conjunto de herramientas de Discovery
{: #integrate-customtooling}

El modelo personalizado de {{site.data.keyword.knowledgestudioshort}} se puede integrar en el enriquecimiento de [Extracción de entidades](/docs/services/discovery?topic=discovery-configservice#entity-extraction) o [Extracción de relaciones](/docs/services/discovery?topic=discovery-configservice#relation-extraction) con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.

No puede aplicar varios modelos personalizados al mismo campo utilizando el conjunto de herramientas de {{site.data.keyword.discoveryshort}}. Se puede aplicar más de un modelo personalizado a campos idénticos utilizando la API. Consulte [Integración de su modelo personalizado con la API](/docs/services/discovery?topic=discovery-integrating-with-wks#integrate-customAPI).

1. Obtenga el `ID de modelo` de su modelo de {{site.data.keyword.knowledgestudioshort}}.
1. En el conjunto de herramientas de {{site.data.keyword.discoveryshort}}, pulse el icono **Gestionar datos** en la parte derecha para abrir la pantalla **Gestionar datos** y, a continuación, cree o abra una colección. **Nota:** Si elige una colección existente, debe estar vacía. Si no lo está, debería volver a ingerir los documentos después de crear el nuevo archivo de configuración.
1. En la sección **Configuración** de la pantalla **Gestionar datos** de su colección, pulse **Conmutar** y, a continuación, **Crear una nueva configuración**. Asigne un nombre a la configuración. 
1. Pulse **Añadir enriquecimientos** y seleccione el enriquecimiento **Extracción de entidades** o **Extracción de relaciones**.
1. Especifique el `ID de modelo` en el recuadro `ID de modelo personalizado` del enriquecimiento seleccionado. El modelo personalizado de {{site.data.keyword.knowledgestudiofull}} prevalecerá sobre el predeterminado para este enriquecimiento. 
1. Pulse **Aplicar** y, a continuación, **Terminado**.

Cuando se cargan documentos en una recopilación de datos, se convierten y enriquecen utilizando el archivo de configuración elegido para dicha recopilación. Si en una recopilación existente cambia a un nuevo archivo de configuración después de haber cargado documentos, estos documentos cargados permanecerán convertidos con el archivo de configuración original. Los documentos cargados después de cambiar el archivo de configuración utilizará el nuevo archivo de configuración. Si desea que **toda** la recopilación utilice la nueva configuración, necesitará crear una nueva recopilación, elegir el nuevo archivo de configuración y volver a cargar todos los documentos.

## Siguientes pasos
{: #wks-nextsteps}

Utilice el servicio {{site.data.keyword.discoveryshort}} con la nueva configuración para ingerir datos privados. Los documentos ingeridos con la configuración actualizada se enriquecerán de forma automática con los datos de su modelo personalizado.

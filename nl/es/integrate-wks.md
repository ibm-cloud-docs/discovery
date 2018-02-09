---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-15"

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

# Integración con Watson Knowledge Studio

Puede integrar un modelo personalizado de {{site.data.keyword.knowledgestudiofull}} con el servicio {{site.data.keyword.discoveryshort}} para proporcionar enriquecimientos personalizados de relaciones y entidades.
{: shortdesc}

Esto ofrece la flexibilidad de aplicar las funcionalidades de mejora de documentos del servicio {{site.data.keyword.discoveryshort}} con información específica de áreas de un tema concreto como, por ejemplo, una disciplina concreta científica o de la industria. Se pueden utilizar tanto datos públicos como sus propios datos privados en el modelo de enriquecimiento. 

Puede utilizar la API del servicio o el conjunto de herramientas de {{site.data.keyword.discoveryshort}} para integrar un modelo de {{site.data.keyword.knowledgestudioshort}} con el servicio de {{site.data.keyword.discoveryshort}}.  

## Antes de empezar

Antes de poder integrar un modelo personalizado de {{site.data.keyword.knowledgestudioshort}} con el servicio {{site.data.keyword.discoveryshort}}, debe crear y desplegar el modelo utilizando {{site.data.keyword.knowledgestudioshort}}. Consulte la [Documentación de {{site.data.keyword.knowledgestudioshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-project.html#wks_tutintro){: new_window} para obtener información sobre cómo crear y desplegar modelos. Necesitará un ID exclusivo del modelo desplegado para integrarlo con el servicio {{site.data.keyword.discoveryshort}}. 

## Integración de su modelo personalizado con la API

1.  Obtenga el ID de su entorno de {{site.data.keyword.discoveryshort}} tal como se describe en [Listar entornos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_environments){: new_window}. Anote el ID de entorno. 
1.  Liste los ID de su configuración o configuraciones de {{site.data.keyword.discoveryshort}} tal como se describe en [Listar configuraciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/discovery/api/v1/#list_configurations){: new_window} Anote el ID de configuración que desea integrar con su modelo personalizado de {{site.data.keyword.knowledgestudiofull}}. 
1.  Descargue una copia de su configuración de {{site.data.keyword.discoveryshort}} actual ejecutando los siguientes mandatos en un shell bash o similar como, por ejemplo Cygwin para Windows. Sustituya `{environment_id}` y `{configuration_id}` con los ID que anotó en los dos pasos anteriores. 

    ```bash
    curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07" > my_config.json
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

1.  Opcionalmente, habilite la normalización de entidad tal como se describe en [Creación de una configuración personalizada para normalizar entidades](/docs/services/discovery/normalize-entities.html). 
1.  Guarde el archivo `my_config.json`. 
1.  Utilice un validador JSON como, por ejemplo [JSLint ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://jslint.com){: new_window} para validarlo y, si es necesario, corrija el JSON editado antes de realizar el siguiente paso. 
1.  Actualice la configuración tal como se indica a continuación. De nuevo necesitará los ID de `{environment_id}` y `{configuration_id}` que recopiló al inicio de este procedimiento. 

    ```bash
    curl -X PUT -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations/{configuration_id}?version=2017-11-07"
    ```
    {: pre}

    **Nota:** Si está creando una nueva configuración, o modificando la configuración predeterminada, deberá crear una nueva configuración personalizada en lugar de actualizar una configuración existente. Antes de crear una nueva configuración, asegúrese de que el campo `"configuration_id":` se elimina del archivo `my_config.json` y luego vuelva a ejecutar el siguiente mandato: 

    ```bash
    curl -X POST -u "{username}":"{password}" -H "Content-Type: application/json" -d @my_config.json "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/configurations?version=2017-11-07"
    ```
    {: pre}

    Ambos mandatos devuelven el contenido del archivo de configuración actualizado. 

## Integración de su modelo personalizado con el conjunto de herramientas de Discovery

El modelo personalizado de {{site.data.keyword.knowledgestudioshort}} se puede integrar en el enriquecimiento de [Extracción de entidades](/docs/services/discovery/building.html#entity-extraction) o [Extracción de relaciones](/docs/services/discovery/building.html#relation-extraction) con el conjunto de herramientas de {{site.data.keyword.discoveryshort}}.          

1. Obtenga el `ID de modelo` de su modelo de {{site.data.keyword.knowledgestudioshort}}. 
1. En el conjunto de herramientas de {{site.data.keyword.discoveryshort}} abra la pantalla **Gestionar datos**, cree o abra una recopilación y cree una nueva configuración. 
1. Pulse **Añadir enriquecimientos** y seleccione el enriquecimiento **Extracción de entidades** o **Extracción de relaciones**. 
1. Especifique el `ID de modelo` en el recuadro `ID de modelo personalizado` del enriquecimiento seleccionado. El modelo personalizado de {{site.data.keyword.knowledgestudiofull}} prevalecerá sobre el predeterminado para este enriquecimiento. Pulse **Aplicar**y, a continuación, **Terminado**.

Cuando se cargan documentos en una recopilación de datos, se convierten y enriquecen utilizando el archivo de configuración elegido para dicha recopilación.  Si en una recopilación existente cambia a un nuevo archivo de configuración después de haber cargado documentos, estos documentos cargados permanecerán convertidos con el archivo de configuración original. Los documentos cargados después de cambiar el archivo de configuración utilizará el nuevo archivo de configuración. Si desea que **toda**
la recopilación utilice la nueva configuración, necesitará crear una nueva recopilación, elegir el nuevo archivo de configuración y volver a cargar todos los documentos. 

**Nota:** Solo se puede asignar un único modelo de {{site.data.keyword.knowledgestudiofull}} a un enriquecimiento. 

## Siguientes pasos

Utilice el servicio {{site.data.keyword.discoveryshort}} con la nueva configuración para ingerir datos privados. Los documentos ingeridos con la configuración actualizada se enriquecerán de forma automática con los datos de su modelo personalizado. 

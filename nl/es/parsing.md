---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-01-15"

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

# Análisis de contratos
{: #contract_parsing}

La Clasificación de elementos devuelve contratos analizados con un análisis de cada elemento identificado.

Las secciones siguientes describen cómo proporciona el análisis el JSON devuelto.

## Tipos
{: #contract_types}

La matriz `types` (tipos) incluye varios objetos, cada uno de los cuales contiene las claves `nature` (naturaleza) y `party` (parte) cuyos valores identifican una dupla para el elemento.

Las tablas siguientes listan los valores posibles de las claves `nature` y `party`.

| `nature` (naturaleza)         |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Definition` (Definición)      |Este elemento añade claridad a un término, relación o similar. No es necesaria ninguna acción para cumplir el elemento, ni está afectada ninguna parte.|
|`Disclaimer` (Descargo de responsabilidad)      |La parte (`party`) del elemento no está obligada a cumplir los términos especificados por el elemento, pero no tiene prohibido hacerlo.|
|`Exclusion` (Exclusión)       |La parte (`party`) del elemento no cumplirá los términos especificados por el elemento.|
|`Obligation` (Obligación)      |La parte (`party`) del elemento necesita cumplir los términos especificados por el elemento.|
|`Right` (Derecho)           |La parte (`party`) del elemento está garantizada para recibir los términos especificados por el elemento.|

Cada clave `nature` se empareja con una clave `party`, que contendrá el nombre o el rol de la parte o las partes que se aplican a la naturaleza (entre los ejemplos se incluyen los siguientes, aunque no se limitan a los mismos: `Buyer` (Comprador), `IBM` o `All Parties` (Todas las partes)). Tenga en cuenta que en la naturaleza `Definition` (Definición), la parte es siempre `None` (Ninguna).

## Partes
{: #contract_parties}

La matriz `parties` (partes) especifica los participantes que están listados en el contrato. Cada objeto `party` está asociado con otros objetos que proporcionan detalles sobre la parte, incluidos:

  - `role`: El rol de la parte. Los valores se listan en la tabla que sigue a esta lista.
  - `importance`: La importancia de la parte. Los valores posibles son `Primary` para una parte primaria y `Unknown` para una parte no primaria.
  - `addresses`: Una matriz que identifica direcciones.
    - `text`: Una dirección.
    - `location`: La ubicación de la dirección como la definen los índices `begin` y `end`.
  - `contacts`: Una matriz que define los nombres y los roles de los contactos identificados en el documento de entrada.
    - `name`: El nombre de un contacto.
    - `role`: El rol del contacto.

Los valores de `role` (rol) que se pueden devolver en los contratos incluyen, entre otros:

| `role` (rol)           |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Buyer` (Comprador)           |La parte responsable de pagar por los productos o servicios que se enumeran en el contrato.|
|`End User` (Usuario final)        |La parte que interactúa con los productos o servicios proporcionados, distinguidos explícitamente del Comprador (`Buyer`).|
|`None` (Ninguno)            |No se ha identificado ninguna parte para el elemento.|
|`Supplier` (Proveedor)        |La parte responsable de proporcionar los productos o servicios que se enumeran en el contrato.|

## Categorías
{: #contract_categories}

La matriz `categories` (categorías) define el tema principal de la frase. 

Las categorías y las descripciones de esta tabla se basan en la legislación de los Estados Unidos y pueden no aplicarse en las jurisdicciones de fuera de los Estados Unidos.
{: important}

Las categorías soportadas actualmente incluyen:

| `categories` (categorías)     |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Amendments` (Enmiendas)      |Elementos que especifican cambios en el contrato una vez que se haya firmado o que se modifiquen en un contrato estándar. Incluye debates de las condiciones para cambiar los términos de contrato.|
|`Asset Use` (Uso de activos)       |Elementos que hacen referencia a la forma en que una parte puede o no utilizar los activos de otra parte. Esto se aplica específicamente a una parte que tenga acceso o que utilice activos como licencias, equipo, herramientas o personal de otra parte durante el proceso de llevar a cabo funciones bajo el acuerdo, incluidos los permisos y las restricciones sobre el mismo.  No se extiende a las especificaciones de las obligaciones de la parte o los derechos en relación con artículos, servicios, licencias, etc., comprados, ya que son los activos propios de la parte, y no los de otra parte.|
|`Assignments` (Asignaciones)     |Elementos que describen la transferencia de derechos, obligaciones o ambos a un tercero.|
|`Audits` (Auditorías)          |Elementos que hacen referencia al derecho de una parte a examinar o revisar la conformidad o los requisitos de que una parte esté disponible para su inspección o revisión de conformidad. Aquí se incluyen las referencias al mantenimiento de registros (principalmente en lo que se refiere al derecho de inspección) y el mantenimiento y retención de los registros de actividad que se pueden examinar.|
|`Business Continuity` (Continuidad del negocio)|Elementos que hacen referencia a las consecuencias si se vende la totalidad de la empresa de una de las partes.|
|`Communication` (Comunicación)  |Elementos que hacen referencia a los requisitos de comunicación, respuesta, notificación o aviso; información de contacto, o información relacionada con los cambios en el contrato. También incluye referencias a los detalles sobre los métodos de comunicación, el acto o proceso de intercambio de información y los medios de intercambio de información aceptables entre las partes (así como otros que no son necesariamente partes directas en el contrato).|
|`Confidentiality` (Confidencialidad) |Elementos que describen cómo pueden o no las partes utilizar la información aprendida en el curso sobre completar un contrato y continuar avanzando. También incluye un debate de la información que se debe mantener confidencial, como guardar secretos comerciales o la no divulgación de información empresarial.|
|`Deliverables` (Entregables)    |Elementos que especifican elementos, como los bienes o servicios, que una parte proporciona a otra bajo los términos del contrato, normalmente a cambio de un pago. Se incluye el debate de la preparación de entregas.|
|`Delivery` (Entrega)        |Elementos que especifican los medios o modos de transferir entregables (cosas, en contraposición a servicios personales) de una parte a otra. Incluye debates de las características de entrega, como la planificación o la ubicación.|
|`Dispute Resolution` (Resolución de disputas)|Elementos que debaten formas de resolver cualquier disputa (por ejemplo, con relación a la mano de obra, las facturas o la facturación) que pueda surgir entre las partes contratantes.  Entre los ejemplos se pueden incluir la solución mediante un procedimiento definido, como un panel de arbitraje, un proceso para obtener una orden judicial, la renuncia al derecho a un juicio o la prohibición de la búsqueda de una acción de clase. También se incluyen referencias a la ley de gobierno del contrato o a la elección de la ley como, por ejemplo, un país o jurisdicción en particular. |
|`Force Majeure` (Fuerza mayor)   |Elementos que hacen referencia a sucesos inesperados o disruptivos fuera del control de la parte que pueden eximir a la parte de cumplir su obligación contractual.|
|`Indemnification` (Indemnización) |Elementos que especifican la corrección de determinadas responsabilidades cuando una parte del contrato se hace responsable de indemnizar a otra parte como resultado de las pérdidas o daños incurridos durante el término, o que surjan de las circunstancias del contrato. También se incluyen referencias a cualquier exención legal de las pérdidas o daños.|
|`Insurance` (Seguros)       |Elementos que hacen referencia a la cobertura de seguro o de términos de cobertura proporcionados por otra parte (incluidos terceros como subcontratistas y otros). Incluye una variedad de seguros, entre los que se incluye, aunque sin limitarse al mismo, el seguro médico.|
|`Intellectual Property` (Propiedad intelectual)|Elementos que tratan la asignación de derechos (como el copyright, las patentes y los secretos comerciales) a las partes del contrato. Incluye patentes, derechos de solicitud para patentes, marcas registradas, nombres comerciales, marcas de servicio, nombres de dominio, derechos de autor y todas las aplicaciones y registros de este tipo de esquemas, modelos industriales, inventos, autoría, invenciones, secretos comerciales, programas de software de computación y otra información de propiedad intangible. También incluye un debate sobre las consecuencias de la violación de los derechos de propiedad intelectual.|
|`Liability` (Responsabilidad)       |Elementos que describen el método para determinar cuándo y cómo se asignan los errores a cualquier parte. Entre los ejemplos se incluyen, aunque sin limitarse a los mismos, declaraciones relativas a las limitaciones de responsabilidad, reclamaciones de terceros y reparaciones, sustituciones o reembolso, según sea necesario, de la parte culpable.|
|`Payment Terms & Billing` (Condiciones de pago y facturación)|Elementos que detallan cómo y cuándo debe pagar o cobrar una parte, así como los elementos o tarifas que las partes pagarán o facturarán. Incluye las referencias a modos o mecanismos de pago.|
|`Pricing & Taxes` (Precios y tasas) |Elementos que hacen referencia a cantidades o figuras asociadas con entregables individuales que se intercambian (por ejemplo, el coste de un elemento concreto) como parte del cumplimiento de los términos del contrato. Incluye referencias a métodos o figuras específicas para calcular precios o importes de impuestos.|
|`Privacy` (Privacidad)         |Elementos que están preocupados por el tratamiento de la información personal confidencial, generalmente en cuanto a su protección (por ejemplo, para satisfacer regulaciones como el GDPR).|
|`Responsibilities` (Responsabilidades)|Elementos que tratan tareas accesorias del contrato que están solo bajo el control de una de las partes, centradas específicamente en el debate de la supervisión de los empleados.|
|`Safety and Security` (Protección y seguridad)|Elementos que hacen referencia a la seguridad física o la protección de seguridad cibernética de personas, datos o sistemas. Entre los ejemplos se encuentran las discusiones sobre comprobaciones de antecedentes, precauciones de seguridad, seguridad de puesto de trabajo, protocolos de acceso seguro y defectos de producto que podrían representar un peligro.|
|`Scope of Work` (Ámbito de trabajo)   |Elementos que definen lo que hay en el contrato en comparación con lo que no está en el contrato; y en consecuencia, lo que se promete que se hará. Entre los ejemplos se incluyen las sentencias que definen un orden determinado o describen las metas u objetivos del contrato.|
|`Subcontracts` (Subcontratos)    |Elementos que hacen referencia a la contratación de terceros para realizar determinadas tareas bajo el contrato, y los permisos, derechos, restricciones y consecuencias relacionadas y que surjan de lo anterior.|
|`Term & Termination` (Término y terminación)|Elementos que hacen referencia a la duración del contrato, la planificación y los términos de la terminación del contrato, y las consecuencias de la terminación, incluidas las obligaciones que se aplican a la terminación o después de la misma.|
|`Warranties` (Garantías)      |Elementos que hacen referencia a promesas y obligaciones en curso realizadas en el contrato que actualmente son verdaderas y seguirán siéndolo en el futuro. También elementos que tratan las consecuencias de romper dichas promesas u obligaciones y los derechos de remediar la situación (por ejemplo, aunque no sin limitarse a la misma, la búsqueda de daños). Esta categoría no se aplica a elementos que están únicamente interesados en la representación de sentencias (sentencias de hechos pasados o presentes) o a elementos que exponen supuestos en relación con sucesos que han ocurrido en el pasado.|

## Atributos
{: #attributes}

La matriz `attributes` (atributos) especifica los atributos identificados en la frase. Cada objeto de la matriz incluye tres claves: `type` (el tipo de atributo de la tabla siguiente), `text` (el texto aplicable) y `location` (los índices `begin` y `end` del atributo del documento de entrada). Los atributos soportados actualmente incluyen:

| `attributes` (atributos)     |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Address` (Dirección)         |Una dirección postal.                                          |
|`Currency` (Moneda)        |Valor monetario y unidades.                                  |
|`DateTime` (Fecha y hora)        |Una fecha, una hora, un rango de fechas o un rango de horas.                   |
|`Location` (Ubicación)        |Una región o ubicación geográfica.                         |
|`Organization` (Organización)    |Una organización.                                           |
|`Person` (Persona)          |Una persona.                                                  |

## Fechas efectivas
{: #effective_dates}

La matriz `effective_dates` (fechas_efectivas) identifica las fechas en las que el documento está en vigor.

| `effective_dates` (fechas_efectivas)|Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`text` (texto)            |Una fecha efectiva, listada como una serie.                     |
|`confidence_level` (nivel_confianza)|El nivel de confianza de la identificación de la fecha efectiva. Los valores posibles son `High` (Alto), `Medium` (Medio) y `Low` (Bajo).|
|`location` (ubicación)        |La ubicación de la fecha como la definen los índices `begin` y `end`.|

## Importes de contrato
{: #contract_amounts}

La matriz `contract_amounts` (importes_contrato) identifica los importes monetarios especificados en el documento.

| `contract_amounts` (importes_contrato)|Descripción                                               |
|:----------------:|-----------------------------------------------------------|
|`text` (texto)            |Un importe de contrato, que aparece listado como una serie.                  |
|`confidence_level` (nivel_confianza)|El nivel de confianza de la identificación del importe del contrato. Los valores posibles son `High` (Alto), `Medium` (Medio) y `Low` (Bajo).|
|`location` (ubicación)        |La ubicación del importe de contrato como lo definen los índices `begin` y `end`.|

## Fechas de terminación
{: #termination_dates}

La matriz `termination_dates` (fechas_terminación) identifica las fechas de terminación del documento.

| `contract_amounts` (importes_contrato)|Descripción                                               |
|:----------------:|-----------------------------------------------------------|
|`text` (texto)            |La fecha de terminación, listada como una serie.                  |
|`confidence_level` (nivel_confianza)|El nivel de confianza de la identificación de la fecha de terminación. Los valores posibles son `High` (Alto), `Medium` (Medio) y `Low` (Bajo).|
|`location` (ubicación)        |La ubicación de la fecha de terminación como la definen los índices `begin` y `end`.|

## Origen
{: #provenance}

Cada objeto de las matrices `types` y `categories` incluye una matriz `provenance_ids` (id_origen). La matriz `provenance_ids` tiene una o varias claves. Cada clave es un valor de hash que puede enviar a IBM para proporcionar comentarios o recibir soporte.

---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-23"

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

# Análisis de contratos
{: #contract_parsing}

La Clasificación de elementos devuelve contratos analizados con un análisis de cada elemento identificado.

Las secciones siguientes describen cómo proporciona el análisis el JSON devuelto.

## Tipos
{: #contract_types}

La matriz `tipos` incluye varios objetos, cada uno de los cuales contiene las claves `naturaleza` y `parte` cuyos valores identifican una dupla para el elemento.

Las tablas siguientes listan los valores posibles de las claves `naturaleza` y `parte`.

| `naturaleza`         |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Definición`      |Este elemento añade claridad a un término, relación o similar. No es necesaria ninguna acción para cumplir el elemento, ni está afectada ninguna parte.|
|`Descargo de responsabilidad`      |La `parte` del elemento no está obligada a cumplir los términos especificados por el elemento, pero no tiene prohibido hacerlo.|
|`Exclusión`       |La `parte` del elemento no cumplirá los términos especificados por el elemento.|
|`Obligación`      |La `parte` del elemento necesita cumplir los términos especificados por el elemento.|
|`Derecho`           |La `parte` del elemento está garantizada para recibir los términos especificados por el elemento.|

Cada clave de `naturaleza` se empareja con una clave de `parte`, que contendrá el nombre o el rol de la parte o las partes que se aplican a la naturaleza (entre los ejemplos se incluyen los siguientes, aunque no se limitan a los mismos: `Comprador`, `IBM` o `Todas las partes`). Tenga en cuenta que en la naturaleza `Definición`, la parte es siempre `Ninguna`.

## Partes
{: #contract_parties}

La matriz `partes` independiente especifica los participantes listados en el contrato. Cada objeto `parte` identificado enumera la parte identificada por nombre y se compara con un `rol` que clasifica el rol del objeto `parte`. Entre los valores de `rol` que se pueden devolver en los contratos se incluyen aunque no se limitan a los mismos:

| `rol`           |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Comprador`           |La parte responsable de pagar por los productos o servicios enumerados en el contrato.|
|`Usuario final`        |La parte que interactuará con los productos o servicios proporcionados, distinguidos explícitamente del `Comprador`.|
|`Ninguno`            |No se ha identificado ninguna parte para el elemento.|
|`Proveedor`        |La parte responsable de proporcionar los productos o servicios enumerados en el contrato.|

## Categorías
{: #contract_categories}

La matriz `categorías` define el tema principal de la frase. Las categorías soportadas actualmente incluyen:

| `categorías`     |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Enmiendas`      |Elementos que especifican cambios en el contrato una vez que se haya firmado o que se modifiquen en un contrato estándar. Incluye debates de las condiciones para cambiar los términos de contrato.|
|`Uso de activos`       |Elementos que hacen referencia a la forma en que una parte puede o no utilizar los activos de otra parte. Esto se aplica específicamente a una parte que tenga acceso o que utilice activos como licencias, equipo, herramientas o personal de otra parte durante el proceso de llevar a cabo funciones bajo el acuerdo, incluidos los permisos y las restricciones sobre el mismo.  No se extiende a las especificaciones de las obligaciones de la parte o los derechos en relación con artículos, servicios, licencias, etc., comprados, ya que son los activos propios de la parte, y no los de otra parte.|
|`Asignaciones`     |Elementos que describen la transferencia de derechos, obligaciones o ambos a un tercero.|
|`Auditorías`          |Elementos que hacen referencia al derecho de una parte a examinar o revisar la conformidad o los requisitos de que una parte esté disponible para su inspección o revisión de conformidad. Aquí se incluyen las referencias al mantenimiento de registros (principalmente en lo que se refiere al derecho de inspección) y el mantenimiento y retención de los registros de actividad que se pueden examinar.|
|`Continuidad del negocio`|Elementos que hacen referencia a las consecuencias si se vende la totalidad de la empresa de una de las partes.|
|`Comunicación`  |Elementos que hacen referencia a los requisitos de comunicación, respuesta, notificación o aviso; información de contacto, o información relacionada con los cambios en el contrato. También incluye referencias a los detalles sobre los métodos de comunicación, el acto o proceso de intercambio de información y los medios de intercambio de información aceptables entre las partes (así como otros que no son necesariamente partes directas en el contrato).|
|`Confidencialidad` |Elementos que describen cómo pueden o no las partes utilizar la información aprendida en el curso sobre completar un contrato y continuar avanzando. También incluye un debate de la información que se debe mantener confidencial, como guardar secretos comerciales o la no divulgación de información empresarial.|
|`Entregables`    |Elementos que especifican elementos, como los bienes o servicios, que una parte proporciona a otra bajo los términos del contrato, normalmente a cambio de un pago. Se incluye el debate de la preparación de entregas.|
|`Entrega`        |Elementos que especifican los medios o modos de transferir entregables (cosas, en contraposición a servicios personales) de una parte a otra. Incluye debates de las características de entrega, como la planificación o la ubicación.|
|`Resolución de disputas`|Elementos que debaten formas de resolver cualquier disputa (por ejemplo, con relación a la mano de obra, las facturas o la facturación) que pueda surgir entre las partes contratantes.  Entre los ejemplos se pueden incluir la solución mediante un procedimiento definido, como un panel de arbitraje, un proceso para obtener una orden judicial, la renuncia al derecho a un juicio o la prohibición de la búsqueda de una acción de clase. También se incluyen referencias a la ley de gobierno del contrato o a la elección de la ley como, por ejemplo, un país o jurisdicción en particular. |
|`Fuerza mayor`   |Elementos que hacen referencia a sucesos inesperados o disruptivos fuera del control de la parte que pueden eximir a la parte de cumplir su obligación contractual.|
|`Indemnización` |Elementos que especifican la corrección de determinadas responsabilidades cuando una parte del contrato se hace responsable de indemnizar a otra parte como resultado de las pérdidas o daños incurridos durante el término, o que surjan de las circunstancias del contrato. También se incluyen referencias a cualquier exención legal de las pérdidas o daños.|
|`Seguros`       |Elementos que hacen referencia a la cobertura de seguro o de términos de cobertura proporcionados por otra parte (incluidos terceros como subcontratistas y otros). Incluye una variedad de seguros, entre los que se incluye, aunque sin limitarse al mismo, el seguro médico.|
|`Propiedad intelectual`|Elementos que tratan la asignación de derechos (como el copyright, las patentes y los secretos comerciales) a las partes del contrato. Incluye patentes, derechos de solicitud para patentes, marcas registradas, nombres comerciales, marcas de servicio, nombres de dominio, derechos de autor y todas las aplicaciones y registros de este tipo de esquemas, modelos industriales, inventos, autoría, invenciones, secretos comerciales, programas de software de computación y otra información de propiedad intangible. También incluye un debate sobre las consecuencias de la violación de los derechos de propiedad intelectual.|
|`Responsabilidad`       |Elementos que describen el método para determinar cuándo y cómo se asignan los errores a cualquier parte. Entre los ejemplos se incluyen, aunque sin limitarse a los mismos, declaraciones relativas a las limitaciones de responsabilidad, reclamaciones de terceros y reparaciones, sustituciones o reembolso, según sea necesario, de la parte culpable.|
|`Condiciones de pago y facturación`|Elementos que detallan cómo y cuándo debe pagar o cobrar una parte, así como los elementos o tarifas que las partes pagarán o facturarán. Incluye las referencias a modos o mecanismos de pago.|
|`Precios y tasas` |Elementos que hacen referencia a cantidades o figuras asociadas con entregables individuales que se intercambian (por ejemplo, el coste de un elemento concreto) como parte del cumplimiento de los términos del contrato. Incluye referencias a métodos o figuras específicas para calcular precios o importes de impuestos.|
|`Privacidad`         |Elementos que están preocupados por el tratamiento de la información personal confidencial, generalmente en cuanto a su protección (por ejemplo, para satisfacer regulaciones como el GDPR).|
|`Responsabilidades`|Elementos que tratan tareas accesorias del contrato que están solo bajo el control de una de las partes, centradas específicamente en el debate de la supervisión de los empleados.|
|`Protección y seguridad`|Elementos que hacen referencia a la seguridad física o la protección de seguridad cibernética de personas, datos o sistemas. Entre los ejemplos se encuentran las discusiones sobre comprobaciones de antecedentes, precauciones de seguridad, seguridad de puesto de trabajo, protocolos de acceso seguro y defectos de producto que podrían representar un peligro.|
|`Ámbito de trabajo`   |Elementos que definen lo que hay en el contrato en comparación con lo que no está en el contrato; y en consecuencia, lo que se promete que se hará. Entre los ejemplos se incluyen las sentencias que definen un orden determinado o describen las metas u objetivos del contrato.|
|`Subcontratos`    |Elementos que hacen referencia a la contratación de terceros para realizar determinadas tareas bajo el contrato, y los permisos, derechos, restricciones y consecuencias relacionadas y que surjan de lo anterior.|
|`Término y terminación`|Elementos que hacen referencia a la duración del contrato, la planificación y los términos de la terminación del contrato, y las consecuencias de la terminación, incluidas las obligaciones que se aplican a la terminación o después de la misma.|
|`Garantías`      |Elementos que hacen referencia a promesas y obligaciones en curso realizadas en el contrato que actualmente son verdaderas y seguirán siéndolo en el futuro. También elementos que tratan las consecuencias de romper dichas promesas u obligaciones y los derechos de remediar la situación (por ejemplo, aunque no sin limitarse a la misma, la búsqueda de daños). Esta categoría no se aplica a elementos que están únicamente interesados en la representación de sentencias (sentencias de hechos pasados o presentes) o a elementos que exponen supuestos en relación con sucesos que han ocurrido en el pasado.|

## Atributos
{: #attributes}

La matriz `atributos` especifica los atributos identificados en la frase. Cada objeto de la matriz incluye tres claves: `type` (el tipo de atributo de la tabla siguiente), `text` (el texto aplicable) y `location` (los índices `begin` y `end` del atributo del documento de entrada). Los atributos soportados actualmente incluyen:

| `atributos`     |Descripción                                                |
|:----------------:|-----------------------------------------------------------|
|`Ubicación`        |Una región o ubicación geográfica.                         |
|`DateTime`        |Una fecha, una hora, un rango de fechas o un rango de horas.                   |
|`Moneda`        |Valor monetario y unidades.                                  |

## Origen
{: #provenance}

Cada objeto de las matrices `types` y `categories` incluye una matriz `provenance_ids`. La matriz `provenance_ids` tiene una o varias claves. Cada clave es un valor de hash que puede enviar a IBM para proporcionar comentarios o recibir soporte.


---
title: "Salidas de Stream Analytics: opciones para almacenamiento y análisis | Microsoft Docs"
description: "Aprenda a seleccionar el destino de las opciones de salida de datos de Stream Analytics, lo que incluye Power BI para los resultados de análisis."
keywords: "transformación de datos, resultados del análisis, opciones de almacenamiento de datos"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Salidas de Stream Analytics: opciones para almacenamiento y análisis
Al crear un trabajo de análisis de transmisiones, tenga en cuenta cómo se consumirán datos resultantes de Hola. ¿Cómo verán resultados de Hola de trabajo de análisis de transmisiones de Hola y donde almacenará?

En orden tooenable una variedad de patrones de aplicación, análisis de transmisiones de Azure tiene distintas opciones para almacenar la salida y ver los resultados del análisis. Esto hace fácil tooview salida del trabajo y le da flexibilidad en el consumo de Hola y el almacenamiento de salida del trabajo Hola para almacenamiento de datos y otros fines. Cualquier salida configurada en el trabajo de hello debe existir antes de inicia el trabajo de Hola y eventos de inicio del flujo. Por ejemplo, si utiliza almacenamiento de blobs como salida, el trabajo de hello no creará una cuenta de almacenamiento automáticamente. Debe toobe creada por el usuario de hello antes de iniciarse el trabajo de hello ASA.

## <a name="azure-data-lake-store"></a>Almacén de Azure Data Lake
Análisis de transmisiones admite el [Almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/). Este almacenamiento le permite toostore los datos de cualquier tamaño, el tipo y la ingesta de velocidad para análisis operativos y exploratorios. Además, toobe de necesidades de análisis de transmisiones había autorizado tooaccess Hola Data Lake Store. Obtener más información sobre la autorización y cómo se tratan los toosign hacia arriba para hello almacén de Data Lake (si es necesario) en hello [Data Lake salida artículo](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Creación de una instancia de Azure Data Lake Store
Cuando se selecciona el almacenamiento de datos Lake como una salida en hello portal de Azure, podrás solicitada tooauthorize una conexión tooan existente almacén de Data Lake.  

![Autorizar el Almacén de Azure Data Lake](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

A continuación, rellene propiedades Hola Hola almacén de Data Lake de salida tal como se muestra a continuación:

![Autorizar el Almacén de Azure Data Lake](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

Hola tabla siguiente enumeran los nombres de propiedad de Hola y su descripción necesarios para crear una salida de almacén de Data Lake.

<table>
<tbody>
<tr>
<td><B>NOMBRE DE LA PROPIEDAD</B></td>
<td><B>DESCRIPCIÓN</B></td>
</tr>
<tr>
<td>Alias de salida</td>
<td>Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis almacén de Data Lake.</td>
</tr>
<tr>
<td>Nombre de cuenta</td>
<td>nombre de Hola de hello cuenta de almacenamiento de datos Lake donde va a enviar el resultado. Aparecerá una lista desplegable de las cuentas de almacén de Data Lake toowhich Hola usuario registrado en el portal de toohello tiene acceso a.</td>
</tr>
<tr>
<td>Patrón de prefijo de la ruta [<I>opcional</I>]</td>
<td>Hola toowrite de ruta de archivo especifican de los archivos dentro de hello cuenta de almacén de Data Lake. <BR>{date}, {time}<BR>Ejemplo 1: carpeta1/registros/{date}/{time}<BR>Ejemplo 2: carpeta1/registros/{date}</td>
</tr>
<tr>
<td>Formato de fecha [<I>opcional</I>]</td>
<td>Si el token de fecha de Hola se usa en la ruta de acceso de prefijo de hello, puede seleccionar formato de fecha de hello en el que se organizan los archivos. Ejemplo: AAAA/MM/DD</td>
</tr>
<tr>
<td>Formato de hora [<I>opcional</I>]</td>
<td>Si el token de tiempo de Hola se usa en la ruta de acceso de prefijo de hello, especifique el formato de hora de hello en el que se organizan los archivos. Actualmente, el valor de hello solo admitido es HH.</td>
</tr>
<tr>
<td>Formato de serialización de eventos</td>
<td>Formato de serialización para los datos de salida. Se admiten JSON, CSV y Avro.</td>
</tr>
<tr>
<td>Codificación</td>
<td>Si el formato CSV o JSON, debe especificarse una codificación. UTF-8 es Hola solo admite el formato de codificación en este momento.</td>
</tr>
<tr>
<td>Delimitador</td>
<td>Solo se aplica para la serialización de CSV. Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos CSV. Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical.</td>
</tr>
<tr>
<td>Formato</td>
<td>Solo se aplica para la serialización de JSON. Separados por líneas Especifica que la salida de hello se formateará haciendo que cada objeto JSON separado por una nueva línea. Matriz especifica que la salida de hello se formateará como una matriz de objetos JSON.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Renovación de la autorización del Almacén de Data Lake
Necesitará toore-autenticar la cuenta de almacén de Data Lake si su contraseña ha cambiado desde que se creó o autenticado por última vez el trabajo.

![Autorizar el Almacén de Azure Data Lake](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>Base de datos SQL
[Base de datos SQL de Azure](https://azure.microsoft.com/services/sql-database/) como salida de datos que son relacionales por naturaleza o de aplicaciones que dependen del contenido hospedado en una base de datos relacional. Trabajos de análisis de transmisiones escribirá tooan de tabla existente en una base de datos de SQL Azure.  Tenga en cuenta ese esquema de tabla Hola debe coincidir exactamente con campos de Hola y sus tipos que se va a utilizar en su trabajo. Un [almacenamiento de datos de SQL Azure](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) también se puede especificar como una salida a través de hello base de datos SQL opción de salida también (esta es una característica de vista previa). tabla de Hello siguiente muestra los nombres de propiedad de Hola y sus descripciones para la creación de una salida de la base de datos SQL.

| Nombre de propiedad | Description |
| --- | --- |
| Alias de salida |Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consultar salida toothis base de datos. |
| Base de datos |nombre de Hola de base de datos de Hola donde va a enviar la salida |
| Nombre del servidor |nombre del servidor de base de datos SQL de Hola |
| Nombre de usuario |nombre de usuario que tiene la base de datos de access toowrite toohello Hola |
| Password |base de datos de Hello contraseña tooconnect toohello |
| Tabla |nombre de la tabla Hola donde se escribirá la salida de hello. nombre de la tabla de Hello distingue mayúsculas de minúsculas y esquema de Hola de esta tabla debe coincidir exactamente toohello número de campos y sus tipos que va a generar la salida del trabajo. |

> [!NOTE]
> Oferta de base de datos de SQL Azure Hola se admite actualmente para una salida de trabajo de análisis de transmisiones. Sin embargo, no se admite una máquina virtual de Azure que ejecute SQL Server con una base de datos asociada. Se trata de asunto toochange en futuras versiones.
> 
> 

## <a name="blob-storage"></a>Almacenamiento de blobs
Almacenamiento de blobs ofrece una solución escalable y rentable para almacenar grandes cantidades de datos no estructurados en la nube de Hola.  Para obtener una introducción en el almacenamiento de blobs de Azure y su uso, vea la documentación de hello en [cómo Blobs toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

tabla de Hello siguiente muestra los nombres de propiedad de Hola y sus descripciones para la creación de una salida de blob.

<table>
<tbody>
<tr>
<td>Nombre de propiedad</td>
<td>Description</td>
</tr>
<tr>
<td>Alias de salida</td>
<td>Se trata de un nombre descriptivo utilizado en el almacenamiento de blobs del toothis de salida de consultas toodirect Hola consulta.</td>
</tr>
<tr>
<td>Cuenta de almacenamiento</td>
<td>nombre de Hola de cuenta de almacenamiento de Hola donde va a enviar el resultado.</td>
</tr>
<tr>
<td>Clave de cuenta de almacenamiento</td>
<td>clave secreta de Hello asociado a la cuenta de almacenamiento de Hola.</td>
</tr>
<tr>
<td>Contenedor de almacenamiento</td>
<td>Los contenedores proporcionan una agrupación lógica para los blobs almacenados en hello servicio de blobs de Microsoft Azure. Al cargar un servicio de blob toohello, debe especificar un contenedor para dicho blob.</td>
</tr>
<tr>
<td>Patrón del prefijo de la ruta de acceso [opcional]</td>
<td>ruta de acceso de archivo Hello usa toowrite los blobs en el contenedor especificado de Hola.<BR>Dentro de la ruta de acceso de hello, puede elegir una o más instancias de hello siguientes 2 variables toospecify Hola frecuencia se escribe los BLOB toouse:<BR>{date}, {time}<BR>Ejemplo 1: cluster1/logs/{date}/{time}<BR>Ejemplo 2: cluster1/logs/{date}</td>
</tr>
<tr>
<td>Formato de fecha [opcional]</td>
<td>Si el token de fecha de Hola se usa en la ruta de acceso de prefijo de hello, puede seleccionar formato de fecha de hello en el que se organizan los archivos. Ejemplo: AAAA/MM/DD</td>
</tr>
<tr>
<td>Formato de hora [opcional]</td>
<td>Si el token de tiempo de Hola se usa en la ruta de acceso de prefijo de hello, especifique el formato de hora de hello en el que se organizan los archivos. Actualmente, el valor de hello solo admitido es HH.</td>
</tr>
<tr>
<td>Formato de serialización de eventos</td>
<td>Formato de serialización para los datos de salida.  Se admiten JSON, CSV y Avro.</td>
</tr>
<tr>
<td>Codificación</td>
<td>Si el formato CSV o JSON, debe especificarse una codificación. UTF-8 es Hola solo admite el formato de codificación en este momento.</td>
</tr>
<tr>
<td>Delimitador</td>
<td>Solo se aplica para la serialización de CSV. Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos CSV. Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical.</td>
</tr>
<tr>
<td>Formato</td>
<td>Solo se aplica para la serialización de JSON. Separados por líneas Especifica que la salida de hello se formateará haciendo que cada objeto JSON separado por una nueva línea. Matriz especifica que la salida de hello se formateará como una matriz de objetos JSON. Esta matriz se cerrarán solo cuando finaliza el trabajo Hola o análisis de transmisiones se movió en toohello siguiente período de tiempo. En general, es línea toouse preferible JSON separado, ya que no requiere ningún tratamiento especial al archivo de salida de hello todavía está escribiendo.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Centro de eventos
[Centros de eventos](https://azure.microsoft.com/services/event-hubs/) es un servicio de introducción de eventos de publicación-suscripción altamente escalable. Puede recopilar millones de eventos por segundo.  Un uso de un concentrador de eventos como salida es resultado de hello de un trabajo de análisis de transmisiones será entrada Hola de otro trabajo de transmisión por secuencias.

Hay unos pocos parámetros que son flujos de datos del centro de eventos de tooconfigure necesarios como salida.

| Nombre de propiedad | Description |
| --- | --- |
| Alias de salida |Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis concentrador de eventos. |
| Espacio de nombres de Bus de servicio |Un espacio de nombres del bus de servicio es un contenedor para un conjunto de entidades de mensajería. Al crear un nuevo Centro de eventos, también se crea un espacio de nombres del Bus de servicio. |
| Centro de eventos |nombre de saludo de la salida del concentrador de eventos |
| Nombre de la directiva del centro de eventos |Hola directiva de acceso compartido, que se puede crear en la pestaña Configurar centro de eventos de Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. |
| Clave de la directiva de centro de eventos |clave de acceso compartido de Hello usa el espacio de nombres de tooauthenticate acceso toohello Bus de servicio |
| Columna Clave de partición [opcional] |Esta columna contiene la clave de partición de hello para la salida del concentrador de eventos. |
| Formato de serialización de eventos |Formato de serialización para los datos de salida.  Se admiten JSON, CSV y Avro. |
| Codificación |Para CSV y JSON, UTF-8 es Hola solo admite el formato de codificación en este momento |
| Delimitador |Solo se aplica para la serialización de CSV. Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos en formato CSV. Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical. |
| Formato |Solo se aplica para el tipo JSON. Separados por líneas Especifica que la salida de hello se formateará haciendo que cada objeto JSON separado por una nueva línea. Matriz especifica que la salida de hello se formateará como una matriz de objetos JSON. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) puede utilizarse como una salida para un tooprovide de trabajo de análisis de transmisiones para una experiencia de visualización enriquecida de resultados del análisis. Esta capacidad puede usarse con paneles operativos, generación de informes e informes basados en métricas.

### <a name="authorize-a-power-bi-account"></a>Autorización de una cuenta de Power BI
1. Cuando se selecciona Power BI como una salida en hello portal de Azure, que se van a ser solicitada tooauthorize un usuario existente de Power BI o toocreate una nueva cuenta de Power BI.  
   
   ![Autorización de un usuario de Power BI](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Cree una cuenta nueva si no aún no tiene una y después haga clic en Autorizar ahora.  Se presenta una pantalla como Hola siguiente.  
   
   ![Cuenta de Power BI de Azure](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. En este paso, proporcionar trabajo Hola cuenta o educativa para autorizar la salida de Power BI Hola. Si aún no se ha registrado en Power BI, elija Registrarse ahora. Hello cuenta profesional o educativa que usa para Power BI podría ser diferente de hello cuenta de suscripción de Azure que ha iniciado sesión.

### <a name="configure-hello-power-bi-output-properties"></a>Configurar las propiedades de salida de hello Power BI
Una vez que tenga cuenta de Power BI Hola autenticado, puede configurar propiedades de hello para el resultado de Power BI. tabla Hello es lista Hola de nombres de propiedad y su descripción tooconfigure el resultado de Power BI.

| Nombre de propiedad | Description |
| --- | --- |
| Alias de salida |Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis salida de Power BI. |
| Área de trabajo de grupo |tooenable compartir datos con otros usuarios de Power BI puede seleccionar cuenta de grupos dentro de Power BI o elegir "Mi área de trabajo" Si no desea que toowrite tooa grupo.  Actualizar un grupo existente, es necesario renovar la autenticación de Power BI de Hola. |
| Nombre del conjunto de datos |Proporcione un nombre de conjunto de datos que se desea para hello Power BI salida toouse |
| Nombre de la tabla |Proporcione un nombre de tabla en conjunto de datos de Hola de hello que Power BI de salida. Actualmente, la salida de Power BI de trabajos de Análisis de transmisiones solo puede tener una tabla en un conjunto de datos. |

Para ver un tutorial de configurar una salida de Power BI y un panel, vea hello [análisis de transmisiones de Azure y Power BI](stream-analytics-power-bi-dashboard.md) artículo.

> [!NOTE]
> No cree explícitamente Hola dataset y tabla en el panel de Power BI Hola. Hello conjunto de datos y tabla se rellenará automáticamente cuando se inicia el trabajo de Hola y trabajo Hola comienza salida bombeo en Power BI. Tenga en cuenta que si la consulta de la tarea de hello no genera los resultados, el conjunto de datos de hello y no se creará la tabla. También tenga en cuenta que si Power BI ya tenía un conjunto de datos y una tabla con hello mismo nombre que Hola uno se proporcionan en este trabajo de análisis de transmisiones, Hola existentes se sobrescribirán.
> 
> 

### <a name="schema-creation"></a>Creación de esquemas
Análisis de transmisiones de Azure crea una tabla en nombre de usuario de Hola y un conjunto de datos de Power BI si no existe. En todos los demás casos, la tabla de Hola se actualiza con nuevos valores. Actualmente, hay una limitación de hello esa solo tabla puede existir dentro de un conjunto de datos.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>Conversión de ASA tooPower BI tipos de datos
Análisis de transmisiones de Azure actualiza el modelo de datos de hello dinámicamente en tiempo de ejecución si los cambios de esquema de salida de hello. Se controlan todos los cambios de nombre de columna, cambios de tipo de columna y Hola adición o eliminación de columnas.

Esta tabla recogen Hola conversiones de tipos de datos de [tipos de datos de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [tipos de Entity Data Model (EDM)](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) si no existe un conjunto de datos de POWER BI y la tabla.


De Stream Analytics | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | string
datetime | DateTime
float | Doble
Matriz de registro | Tipo cadena, valor constante “IRecord” o “IArray”

### <a name="schema-update"></a>Actualización de esquema
Análisis de transmisiones deduce el esquema de modelo de datos de hello basada en hello primer conjunto de eventos de salida de hello. Más adelante, si es necesario, esquema de modelo de datos de hello está actualizada tooaccommodate eventos entrantes que no caben en el esquema original de Hola.

Hola `SELECT *` consulta debería evitarse tooprevent actualizar el esquema dinámico en filas. Además toopotential implicaciones de rendimiento, lo también podrían indeterminacy de tiempo Hola de resultados de Hola. deben seleccionar campos exactos de Hola que necesitan toobe que se muestra en el panel de Power BI. Además, los valores de datos de hello deben ser compatibles con hello elegido el tipo de datos.


Anterior o actual | Int64 | string | DateTime | Doble
-----------------|-------|--------|----------|-------
Int64 | Int64 | String | string | Doble
Doble | Doble | string | string | Doble
string | String | String | String |  | string | 
DateTime | string | string |  DateTime | String


### <a name="renew-power-bi-authorization"></a>Renovación de la autorización de Power BI
Necesitará toore-autenticar la cuenta de Power BI si su contraseña ha cambiado desde que se creó o autenticado por última vez el trabajo. Si la autenticación multifactor (MFA) está configurado en el inquilino de Azure Active Directory (AAD) también necesitará autorización de Power BI toorenew cada 2 semanas. Un síntoma de este problema es ninguna salida de trabajo y un "error de usuario de autenticar" en los registros de operaciones de hello:

  ![Error de token de actualización de Power BI](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve este problema, detenga el trabajo en ejecución y vaya tooyour salida de Power BI.  Haga clic en el vínculo de "Autorización Renew" hello y reiniciar el trabajo de hello pérdida de datos de tooavoid de última hora de detención.

  ![Autorización de renovación de Power BI](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Table Storage
[El almacenamiento de tabla](../storage/common/storage-introduction.md) ofrece un almacenamiento altamente disponible y escalable de forma masiva, para que una aplicación puede escalar automáticamente toomeet demanda de los usuarios. Almacenamiento de tabla es almacén de clave/atributo NoSQL de Microsoft que puede aprovechar para datos estructurados con menos restricciones en el esquema de Hola. El almacenamiento de tabla puede ser datos de toostore utilizado para la persistencia y la recuperación eficaz.

Hola tabla siguiente enumeran los nombres de propiedad de Hola y sus descripciones para la creación de una salida de la tabla.

| Nombre de propiedad | Description |
| --- | --- |
| Alias de salida |Se trata de un nombre descriptivo utilizado en el almacenamiento de tabla toothis de consultas toodirect Hola consulta salida. |
| Cuenta de almacenamiento |nombre de Hola de cuenta de almacenamiento de Hola donde va a enviar el resultado. |
| Clave de cuenta de almacenamiento |tecla de acceso de Hello asociado a la cuenta de almacenamiento de Hola. |
| Nombre de la tabla |nombre de Hola de tabla de Hola. tabla de Hello obtener creará si no existe. |
| Partition Key |nombre de Hola de columna de salida Hola contenedor clave de partición Hola. clave de partición de Hello es un identificador único para la partición de hello en una tabla determinada que forma Hola primera parte de la clave principal de una entidad. Es un valor de cadena que puede ser up too1 KB de tamaño. |
| Row Key |nombre de Hola de columna de salida Hola contenedor clave de fila Hola. clave de fila de Hello es un identificador único para una entidad en una partición determinada. Lo constituye Hola segunda parte de la clave principal de una entidad. clave de fila de Hello es un valor de cadena que puede ser up too1 KB de tamaño. |
| Tamaño de lote |número de Hola de registros para una operación por lotes. Normalmente predeterminado hello es suficiente para la mayoría de los trabajos, consulte toohello [especificación de operación de lote de tabla](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) para obtener más información acerca de cómo modificar esta configuración. |

## <a name="service-bus-queues"></a>Colas de Service Bus
[Colas de Service Bus](https://msdn.microsoft.com/library/azure/hh367516.aspx) ofrecen un primero en ENTRAR, primero en salir (FIFO) mensaje entrega tooone o varios consumidores en competencia. Mensajes no suelen toobe esperado recibe y procesa los receptores de hello en orden temporal de hello en el que se agregaron toohello cola, y cada mensaje lo recibe y procesa un consumidor de mensajes solo una.

tabla de Hello siguiente muestra los nombres de propiedad de Hola y sus descripciones para la creación de una salida de la cola.

| Nombre de propiedad | Description |
| --- | --- |
| Alias de salida |Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis cola de Bus de servicio. |
| Espacio de nombres de Bus de servicio |Un espacio de nombres del bus de servicio es un contenedor para un conjunto de entidades de mensajería. |
| Nombre de la cola |nombre de Hola de hello cola de Bus de servicio. |
| Nombre de la directiva de colas |Cuando se crea una cola, también puede crear directivas de acceso compartido en la pestaña configurar cola de Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. |
| Clave de la directiva de colas |clave de acceso compartido de Hello usa el espacio de nombres de tooauthenticate acceso toohello Bus de servicio |
| Formato de serialización de eventos |Formato de serialización para los datos de salida.  Se admiten JSON, CSV y Avro. |
| Codificación |Para CSV y JSON, UTF-8 es Hola solo admite el formato de codificación en este momento |
| Delimitador |Solo se aplica para la serialización de CSV. Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos en formato CSV. Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical. |
| Formato |Solo se aplica para el tipo JSON. Separados por líneas Especifica que la salida de hello se formateará haciendo que cada objeto JSON separado por una nueva línea. Matriz especifica que la salida de hello se formateará como una matriz de objetos JSON. |

## <a name="service-bus-topics"></a>Temas de Service Bus
Mientras que las colas de Service Bus ofrecen un método de comunicación tooone uno de remitente tooreceiver, [Service Bus Topics](https://msdn.microsoft.com/library/azure/hh367516.aspx) proporcionan una forma de comunicación uno a varios.

Hola tabla siguiente enumeran los nombres de propiedad de Hola y sus descripciones para la creación de una salida de la tabla.

| Nombre de propiedad | Description |
| --- | --- |
| Alias de salida |Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis tema de Bus de servicio. |
| Espacio de nombres de Bus de servicio |Un espacio de nombres del bus de servicio es un contenedor para un conjunto de entidades de mensajería. Al crear un nuevo Centro de eventos, también se crea un espacio de nombres del Bus de servicio. |
| Nombre del tema |Los temas son mensajería entidades, los centros de tooevent similar y colas. Se trata de secuencias de eventos de toocollect diseñado de una serie de diferentes dispositivos y servicios. Cuando se crea un tema, se proporciona también un nombre específico. mensajes de saludo envían tooa tema no estará disponible a menos que se crea una suscripción, asegúrese de modo que hay una o varias suscripciones bajo tema Hola |
| Nombre de la directiva de temas |Cuando se crea un tema, también puede crear directivas de acceso compartido en la pestaña configurar tema de Hola. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. |
| Clave de la directiva de temas |clave de acceso compartido de Hello usa el espacio de nombres de tooauthenticate acceso toohello Bus de servicio |
| Formato de serialización de eventos |Formato de serialización para los datos de salida.  Se admiten JSON, CSV y Avro. |
| Codificación |Si el formato CSV o JSON, debe especificarse una codificación. UTF-8 es Hola solo admite el formato de codificación en este momento |
| Delimitador |Solo se aplica para la serialización de CSV. Análisis de transmisiones admite un número de delimitadores comunes para la serialización de datos en formato CSV. Los valores admitidos son la coma, punto y coma, espacio, tabulador y barra vertical. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) es un servicio de base de datos de documentos NoSQL totalmente administrado que ofrece consultas y transacciones a través de datos sin esquema, rendimiento predecible y confiable y desarrollo rápido.

Hola por debajo de los nombres de propiedad de lista detalles hello y sus descripciones para la creación de una salida de la base de datos de Azure Cosmos.

* **Alias de salida** – un toorefer alias este resultado de la consulta ASA  
* **Nombre de cuenta** : nombre de Hola o extremo URI de hello cuenta de base de datos de Cosmos.  
* **Clave de cuenta** : clave de acceso compartido de Hola para hello cuenta de base de datos de Cosmos.  
* **Base de datos** : nombre de base de datos de base de datos de Cosmos Hola.  
* **Patrón de nombre de colección** : nombre de la colección de Hola o su patrón de hello colecciones toobe usa. formato de nombre de colección de Hello puede crearse mediante token {partition} opcional de hello, donde se inician las particiones desde 0. Las siguientes entradas de ejemplo son válidas:  
  1\) MyCollection: debe existir una colección denominada "MyCollection".  
  2\) MyCollection{partición}: deben existir esas colecciones: "MyCollection0", "MyCollection1", "MyCollection2", etc.  
* **Clave de partición**: opcional. Solo es necesario si usa un token {partition} en el patrón de nombre de la colección. nombre de Hello del campo de hello en toospecify Hola clave de salida eventos que se usa para crear particiones de salida de todas las colecciones. Para una salida de colección sencilla, se puede utilizar cualquier columna de salida arbitraria (por ejemplo, PartitionId).  
* **Identificador de documento** : opcional. nombre de Hola de campo de hello en los eventos de salida utiliza la clave principal de toospecify hello en las instrucciones insert o update se basan las operaciones.  


## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
Ha estado tooStream se ha introducido el análisis, un servicio administrado para analizar los datos de Internet de las cosas Hola de transmisión por secuencias. toolearn más información acerca de este servicio, vea:

* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

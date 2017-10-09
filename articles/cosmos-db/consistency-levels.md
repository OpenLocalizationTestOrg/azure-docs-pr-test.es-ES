---
title: niveles de aaaConsistency en la base de datos de Azure Cosmos | Documentos de Microsoft
description: Base de datos de Azure Cosmos tiene cinco coherencia niveles toohelp saldo final coherencia, la disponibilidad y la latencia ventajas e inconvenientes.
keywords: coherencia final, azure cosmos db, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Niveles de coherencia de datos optimizables en Azure Cosmos DB
Base de datos de Azure Cosmos está diseñado de hello descárguese de corriente con la distribución global en cuenta para cada modelo de datos. Es toooffer diseñada garantías de predicción de baja latencia, un SLA de disponibilidad del 99,99%, y varios bien definido redujeron los modelos de coherencia. Actualmente, Azure Cosmos DB ofrece cinco niveles de coherencia: fuerte, de obsolescencia limitada, de sesión, de prefijo coherente y final. 

Además de los modelos de **coherencia fuerte** y **final** que proporcionan habitualmente las bases de datos distribuidas, Azure Cosmos DB ofrece tres modelos de coherencia codificados y operacionalizados de forma cuidadosa. Además, tiene su utilidad validada en casos de uso reales. Se trata de hello **limitado obsolescencia**, **sesión**, y **prefijo coherente** niveles de coherencia. Colectivamente estos niveles de cinco coherencia permiten toomake bien motivada ventajas y desventajas de coherencia, la disponibilidad y la latencia. 

## <a name="distributed-databases-and-consistency"></a>Coherencia y bases de datos distribuidas
Las bases de datos distribuidas comerciales se dividen en dos categorías: las bases de datos que no ofrecen opciones de coherencia bien definida en absoluto y las que ofrecen dos opciones de programación opuestas (coherencia alta y ocasional). 

Hola a los desarrolladores de aplicaciones de cargas de trabajo anterior con minucias de los protocolos de replicación y ellos no espera toomake difícil contrapartidas entre coherencia, disponibilidad, latencia y rendimiento. Hola este último coloca un toochoose presión uno de los dos extremos de Hola. A pesar del gran cantidad de Hola de investigación y propuestas de más de 50 modelos de coherencia, hello Comunidad de base de datos distribuida no ha sido capaz de toocommercialize niveles de coherencia más allá de coherencia eventual y seguro. COSMOS DB permite a los desarrolladores toochoose entre cinco modelos bien definidos de coherencia en el espectro de coherencia de hello: seguro, limitado obsolescencia, [sesión](http://dl.acm.org/citation.cfm?id=383631), prefijo coherente y final. 

![Base de datos de Azure Cosmos ofrece varios, bien definida toochoose de modelos de coherencia (estrictas) de](./media/consistency-levels/five-consistency-levels.png)

Hello en la tabla siguiente muestra garantías particulares Hola que ofrece cada nivel de coherencia.
 
**Niveles de coherencia y garantías**

| Nivel de coherencia | Garantías |
| --- | --- |
| Alta | Linealidad |
| De obsolescencia entrelazada | Prefijo coherente. Los prefijos k y los intervalos t retrasan las lecturas tras las escrituras |
| Sesión   | Prefijo coherente. Lecturas monótonas, escrituras monótonas, lectura de la escritura, escritura tras las lecturas |
| De prefijo coherente | Actualizaciones devueltas son algunos prefijo de todas las actualizaciones de hello, con no vacíos |
| Ocasional  | Lecturas sin orden |

Puede configurar el nivel de coherencia de hello predeterminado en su cuenta de base de datos de Cosmos (y más adelante invalidar la coherencia de Hola de una solicitud de lectura específica). Internamente, nivel de coherencia de hello predeterminado aplica toodata dentro de los conjuntos de particiones de Hola que puede abarcar varias regiones. Aproximadamente un 73 % de nuestros inquilinos usan la coherencia de sesión y un 20 % prefiere la obsolescencia limitada. Observamos que aproximadamente el 3 % de nuestros clientes experimentan con distintos niveles de coherencia inicialmente antes de fijar una opción de coherencia específica para su aplicación. También observamos que solo un 2 % de nuestros inquilinos reemplazan los niveles de coherencia por solicitud. 

En Cosmos DB, las lecturas de coherencia de sesión, prefijo coherente y final son el doble de económicas que las de coherencia fuerte o de obsolescencia limitada. Cosmos DB presenta acuerdos de nivel de servicio líderes del sector completos del 99,99 %, que incluyen garantías de coherencia, además de disponibilidad, rendimiento y latencia. Empleamos una [Comprobador linearizability](http://dl.acm.org/citation.cfm?id=1806634), que funciona continuamente a través de nuestro telemetría de servicio e informa abiertamente cualquier tooyou de infracciones de coherencia. Para limitado obsolescencia, hemos supervisar y notificar las infracciones de tardaron y límites de t. Para todos los cinco niveles de coherencia no estricta, también se informa de hello [métrica de uso vinculado probabilística](http://dl.acm.org/citation.cfm?id=2212359) tooyou directamente.  

## <a name="scope-of-consistency"></a>Ámbito de coherencia
granularidad de Hola de coherencia es ámbito tooa solicitud de usuario único. Una solicitud de escritura puede ser corresponden tooan Insertar, reemplazar, upsert o eliminar la transacción. Al igual que con operaciones de escritura, una transacción de lectura o consulta también es tooa ámbito solicitud de usuario único. usuario de Hello puede ser necesario toopaginate sobre un gran conjunto de resultados, que abarcan varias particiones, pero cada uno, leen transacción está en ámbito tooa sola página y servirse desde dentro de una sola partición.

## <a name="consistency-levels"></a>Niveles de coherencia
Puede configurar un nivel de coherencia de manera predeterminada en la cuenta de base de datos que se aplica a las colecciones de tooall (y las bases de datos) en su cuenta de base de datos de Cosmos. De forma predeterminada, todas las lecturas y las consultas emitidas en hello nivel de coherencia de hello predeterminado especificado en la cuenta de base de datos de hello utilizan recursos definidos por el usuario. Pueden ser menos exigentes de nivel de coherencia de Hola de una lectura/consulta específica admite el uso de cada uno de hello las API de solicitud. Hay cinco tipos de niveles de coherencia compatibles con protocolo de replicación de base de datos de Azure Cosmos Hola que proporcionan una solución de compromiso clara entre garantías de coherencia específico y el rendimiento, como se describe en esta sección.

**Alta**: 

* Coherencia fuerte ofrece un [linearizability](https://aphyr.com/posts/313-strong-consistency-models) garantía con hello lee la versión más reciente de hello tooreturn garantizada de un elemento. 
* Coherencia fuerte garantiza que una operación de escritura solo está visible después de su duración confirmada por quórum de mayoría de Hola de réplicas. Una operación de escritura o sincrónicamente duración confirmada Hola principal y quórum Hola de servidores secundarios, o se anula. Leer el quórum de mayoría de hello siempre confirma una lectura, un cliente nunca puede ver una escritura sin confirmar o parcial y se garantiza que siempre tooread hello más reciente confirmados escritura. 
* Azure cuentas de base de datos de Cosmos homogeneidad toouse configurado no pueden asociar más de una región de Azure con su cuenta de base de datos de Azure Cosmos. 
* Hola costo de una operación de lectura (en términos de [unidades de solicitud](request-units.md) consumido) con coherencia fuerte es mayor que la sesión y final, pero Hola igual como uso vinculado.

**De obsolescencia entrelazada**: 

* Coherencia de uso vinculado garantiza que las lecturas Hola pueden retrasarse a lo sumo escrituras *K* versiones o prefijos de un elemento o *t* intervalo de tiempo. 
* Por lo tanto, cuando elige limitado obsolescencia, Hola "obsolescencia" puede configurarse de dos maneras: número de versiones *K* de elemento de hello mediante el cual Hola lecturas retrasen escrituras de Hola y el intervalo de tiempo de hello *t* 
* Limitado obsolescencia ofrece total orden global excepto dentro de Hola "ventana de obsolescencia". Hola monotónico lee garantías existe dentro de una región tanto dentro como fuera Hola "ventana de obsolescencia". 
* La obsolescencia entrelazada proporciona una garantía de coherencia más fuerte que la coherencia de sesión o la eventual. Para las aplicaciones distribuidas globalmente, se recomienda que utilizar obsolescencia limitada para escenarios donde tendrían como toohave homogeneidad pero también desea latencia baja y una disponibilidad del 99,99%. 
* Las cuentas de Azure Cosmos DB que están configuradas con la coherencia de obsolescencia limitada pueden asociar cualquier número de regiones de Azure a su cuenta de Azure Cosmos DB. 
* Hola costo de una operación de lectura (en términos de RUs consumido) con uso vinculado es mayor que la sesión y la coherencia, pero Hola igual como homogeneidad.

**Sesión**: 

* A diferencia de los modelos de coherencia global Hola ofrecidos por los niveles de coherencia de obsolescencia segura y sin enlazar, coherencia de la sesión es la sesión de cliente de tooa con ámbito. 
* La coherencia de sesión es ideal para todos los escenarios en los que exista una sesión de usuario o dispositivo, ya que garantiza lecturas monotónicas, escrituras monotónicas y lectura de sus propias escrituras (RYW). 
* Coherencia de la sesión proporciona una coherencia de predicción para una sesión y máximo rendimiento de lectura al tiempo que ofrece lecturas y escrituras de latencia más bajos de Hola. 
* Las cuentas de Azure Cosmos DB que están configuradas con la coherencia de sesión pueden asociar cualquier número de regiones de Azure a su cuenta de Azure Cosmos DB. 
* Hola costo de una operación de lectura (en términos de RUs consumido) con el nivel de coherencia es menor que la obsolescencia segura y sin enlazar, pero más de la coherencia de sesión

<a id="consistent-prefix"></a>
**De prefijo coherente**: 

* Prefijo coherente garantiza que en ausencia de otras escrituras, las réplicas de hello en grupo de hello finalmente convergen. 
* El prefijo coherente garantiza que las lecturas nunca vean escrituras desordenadas. Si se realizan escrituras en orden de hello `A, B, C`, a continuación, un cliente ve bien `A`, `A,B`, o `A,B,C`, pero nunca fuera de servicio como `A,C` o `B,A,C`.
* Las cuentas de Azure Cosmos DB que están configuradas con la coherencia de prefijo coherente pueden asociar cualquier número de regiones de Azure a su cuenta de Azure Cosmos DB. 

**Ocasional**: 

* Coherencia definitiva garantiza que en ausencia de otras escrituras, las réplicas de hello en grupo de hello finalmente convergen. 
* Coherencia definitiva es la forma más débil de Hola de coherencia donde un cliente puede obtener valores de hello que sean más antiguos que Hola que había visto antes.
* Coherencia definitiva proporciona coherencia de lectura de hello más débil, pero ofrece hello latencia más baja para lecturas y escrituras.
* Las cuentas de Azure Cosmos DB que están configuradas con la coherencia final pueden asociar cualquier número de regiones de Azure a su cuenta de Azure Cosmos DB. 
* Hola costo de una operación de lectura (en términos de RUs consumido) con coherencia definitiva Hola nivel es el menor de todos los niveles de coherencia de base de datos de Azure Cosmos Hola Hola.

## <a name="configuring-hello-default-consistency-level"></a>Configurando el nivel de coherencia de saludo predeterminado
1. Hola [portal de Azure](https://portal.azure.com/), en Hola Jumpbar, haga clic en **base de datos de Azure Cosmos**.
2. Hola **base de datos de Azure Cosmos** hoja, toomodify de cuenta de base de datos de hello select.
3. En la hoja de la cuenta de hello, haga clic en **predeterminado coherencia**.
4. Hola **coherencia predeterminada** hoja, nivel de coherencia de hello seleccione Nuevo y haga clic en **guardar**.
   
    ![Captura de pantalla de resaltado de icono de configuración de Hola y entrada de coherencia predeterminada](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Niveles de coherencia para consultas
De forma predeterminada, para los recursos definidos por el usuario, nivel de coherencia de Hola para consultas es Hola mismo tal y como se lee de nivel de coherencia de Hola para. De forma predeterminada, índice Hola se actualiza de forma sincrónica en cada inserción, sustitución o eliminación de un contenedor de elemento toohello Cosmos DB. Esto permite que las consultas de hello toohonor Hola de mismo nivel de coherencia de punto de lecturas. Mientras la base de datos de Azure Cosmos es de escritura optimizado y admite volúmenes sostenidos de escrituras, el mantenimiento del índice sincrónicas y atender consultas coherente, puede configurar cierto tooupdate colecciones su índice de forma diferida. Aún más la indexación diferida mejora el rendimiento de escritura de Hola y es ideal para escenarios de ingesta de forma masiva cuando una carga de trabajo es principalmente con muchas lecturas.  

| Modo de indexación | Lecturas | Consultas |
| --- | --- | --- |
| Coherente (predeterminado) |Seleccionar entre fuerte, de obsolescencia limitada, de sesión, de prefijo coherente o final |Seleccionar entre fuerte, de obsolescencia entrelazada, de sesión y eventual |
| Diferida |Seleccionar entre fuerte, de obsolescencia limitada, de sesión, de prefijo coherente o final |Ocasional |
| None |Seleccionar entre fuerte, de obsolescencia limitada, de sesión, de prefijo coherente o final |No aplicable |

Como con las solicitudes de lectura, puede disminuir nivel de coherencia de Hola de una solicitud de consulta específica en cada API.

## <a name="next-steps"></a>Pasos siguientes
Si desea que toodo leer más sobre los niveles de coherencia y compensaciones, se recomienda Hola recursos siguientes:

* Doug Terry. Vídeo Replicated Data Consistency explained through baseball (Coherencia de datos replicados explicada mediante el béisbol).   
  [https://www.youtube.com/watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. Explicación de la coherencia de datos replicados a través del béisbol.   
  [http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. Garantías de sesión para datos replicados con coherencia débil.   
  [http://dl.acm.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. Inconvenientes de coherencia moderna diseñar sistemas de bases de datos distribuidas: CAP es solo una parte de caso de Hola ".   
  [http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica. Uso vinculado probabilístico (PBS) para cuórums parciales prácticos.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Coherencia ocasional - Revisión.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.html](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* MONI Naor, Avishai en rama, Hola carga, capacidad y disponibilidad de quórum sistemas SIAM diario en informática, n.2 v.27, p.423-447, abril de 1998.
  [http://epubs.siam.org/doi/abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Roy Tan, línea: un completo y automática linearizability Comprobador, actas de conferencia de ACM SIGPLAN 2010 hello en Programming language diseño e implementación, 05-10 de junio de 2010, Toronto, Ontario, Canadá [dominio de interpretación > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica, probabilísticamente limitado obsolescencia de prácticas quórums parciales, un procedimiento de hello Almacenamientos dotación, v.5 n.8, p.776-787, abril de 2012 [http:// DL.ACM.org/Citation.cfm?ID=2212359](http://dl.acm.org/citation.cfm?id=2212359)

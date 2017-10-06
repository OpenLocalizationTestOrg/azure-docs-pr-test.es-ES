---
title: arquitectura de Azure Active Directory aaaUnderstand | Documentos de Microsoft
description: "Explica qué es un inquilino de Azure AD y cómo toomanage Azure a través de Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Información sobre la arquitectura de Azure Active Directory
Habilita el Azure Active Directory (Azure AD) toosecurely administrar acceso tooAzure servicios y recursos para los usuarios. Con Azure AD se incluye un conjunto completo de funcionalidades de administración de identidades. Para más información sobre las características de Azure AD, consulte [¿Qué es Azure Active Directory?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)

Con Azure AD, puede crear y administrar usuarios y grupos y habilitar permisos tooallow y denegar el acceso a recursos de tooenterprise. Para obtener información acerca de la administración de identidad, vea [Hola aspectos básicos de la administración de identidades de Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Arquitectura de Azure AD
Arquitectura distribuida geográficamente de Azure AD combina amplio de supervisión, reenrutamiento automatizada, la conmutación por error y capacidades de recuperación nos permiten a los clientes de tooour de disponibilidad y rendimiento de nivel empresarial toodeliver.

Hola después de elementos de la arquitectura se trata en este artículo:
 *  Diseño de la arquitectura del servicio
 *  Escalabilidad 
 *  Disponibilidad continua
 *  Centros de datos

### <a name="service-architecture-design"></a>Diseño de la arquitectura del servicio
Hola más comunes forma toobuild un sistema escalable, alta disponibilidad, con datos completos de datos es a través de bloques de creación independientes o unidades de escalado para la capa de datos de Azure AD hello, unidades de escala se denominan *particiones*. 

capa de datos de Hello tiene varios servicios front-end que proporcionan la capacidad de lectura y escritura. diagrama de Hello siguiente muestra cómo se distribuyen los componentes de Hola de una partición de directorio único a lo largo de centros de datos geográficamente distribuido. 

  ![Particiones de directorio único](./media/active-directory-architecture/active-directory-architecture.png)

componentes de Hola de arquitectura de Azure AD incluyen una réplica principal y las réplicas secundarias.

**Réplica principal**

Hola *réplica principal* todos los recibe *escribe* de partición de Hola que pertenece. Cualquier escritura operación es tooa inmediatamente replicados réplica secundaria en otro centro de datos antes de devolver el éxito toohello autor de la llamada, lo que garantiza la durabilidad de las escrituras con redundancia geográfica.

**Réplicas secundarias**

Todas las *lecturas* de los directorios son atendidas desde las *réplicas secundarias*, que se encuentran en centros de datos ubicados físicamente en regiones geográficas diferentes. Existen muchas réplicas secundarias, ya que los datos se replican de forma asincrónica. Lecturas de directorio, como las solicitudes de autenticación, se procesan desde los centros de datos que son clientes de tooour cerrar. las réplicas secundarias de Hello son responsables de escalabilidad de lectura.

### <a name="scalability"></a>Escalabilidad

Escalabilidad es la capacidad de Hola de un toomeet de tooexpand servicio crecientes demandas de rendimiento. Escribir la escalabilidad se consigue mediante la partición datos Hola. Escalabilidad de lectura se logra al replicar datos de réplicas secundarias de una partición toomultiple distribuidas a lo largo de Hola a todos.

Las solicitudes de directorio de aplicaciones son centro de datos de toohello generalmente enrutado que está físicamente cercanos. Las escrituras son coherencia de lectura y escritura de tooprovide de toohello redirige de forma transparente réplica principal. Las réplicas secundarias amplían significativamente escala Hola de particiones como directorios de hello suelen tener lecturas atendiendo la mayoría de las veces de Hola.

Directorio de aplicaciones conectarse toohello más cercano de los centros de datos. Esto mejora el rendimiento y, por tanto, es posible el escalado horizontal. Dado que una partición de directorio puede tener muchas de las réplicas secundarias, las réplicas secundarias pueden colocarse a más cerca de clientes de directorio toohello. Solo interno directory service components que forman réplica principal de destino de escritura intensiva Hola activa directamente.

### <a name="continuous-availability"></a>Disponibilidad continua

Disponibilidad (o el tiempo de actividad) define la capacidad de Hola de un tooperform sistema sin interrupciones. Hola clave tooAzure de AD de alta disponibilidad es que nuestros servicios pueden cambiar rápidamente el tráfico a través de varios centros de datos distribuidos geográficamente. Cada centro de datos es independiente, lo que permite anular la correlación de los modos con error.

Diseño de la partición de Azure AD es enterprise toohello comparados simplificado diseño de AD, lo cual resulta esencial para escalar el sistema de Hola. Hemos adoptado un diseño con un único servidor principal que incluye un proceso de conmutación por error de la réplica principal determinista y cuidadosamente organizado.

**Tolerancia a errores**

Un sistema ya están disponible si es tolerante a errores de toohardware, red y software. Para todas las particiones de directorio de hello, existe una alta disponibilidad réplica principal: réplica principal de Hola. Solo escribe toohello partición se realizan en esta réplica. Esta réplica es que se supervisan continuamente y estrechamente y escribe puede ser tooanother inmediatamente desplazadas réplica (que se convierte en hello nuevo elemento principal) si se detecta un error. Durante la conmutación por error, podría haber una pérdida de disponibilidad de escritura de 1 a 2 minutos. La disponibilidad de lectura no se ve afectada durante este tiempo.

Las operaciones de lectura (que superar a las escrituras en muchas órdenes de magnitud) sólo van toosecondary réplicas. Puesto que las réplicas secundarias son idempotentes, pérdida de alguna réplica de una en una partición determinada se compensa fácilmente dirigiendo Hola lecturas tooanother réplica, normalmente Hola mismo centro de datos.

**Durabilidad de datos**

Una operación de escritura es duradera tooat dos menos datos centros anterior tooit va a reconocer. Esto ocurre por confirmar en primer lugar escritura hello en hello principal y, a continuación, inmediatamente replicar Hola escritura tooat menos un otro centro de datos. Esto garantiza que un potencial de pérdida grave de Hola datos center hospedaje Hola principal no se produce pérdida de datos.

Azure AD mantiene un cero [objetivo de tiempo de recuperación (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) de emisión de tokens y directorio lee y en orden de Hola de minutos (5 minutos) en RTO para directorio escribe. También mantenemos un [objetivo de punto de recuperación (RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective) cero y no se perderán datos en las conmutaciones por error.

### <a name="data-centers"></a>Centros de datos

Réplicas de Azure AD se almacenan en los centros de datos que se encuentran a lo largo de Hola a todos. Para más información, consulte [Centros de datos de Azure](https://azure.microsoft.com/en-us/overview/datacenters).

Azure AD funciona a través de centros de datos con hello siguientes características:

 * Autenticación, gráfico y otros servicios de AD residen detrás Hola servicio de puerta de enlace. Hola puerta de enlace administra el equilibrio de carga de estos servicios. Conmutará por error automáticamente si se detecta algún servidor incorrecto mediante el sondeo de estado transaccional. En función de estas comprobaciones de mantenimiento, Hola puerta de enlace dinámicamente enruta tráfico toohealthy los centros de datos.
 * Para *lee*, el directorio de hello tiene réplicas secundarias y los correspondientes servicios front-end en una configuración activo / activo funciona en varios centros de datos. En caso de error de un centro de datos completo, el tráfico será tooa enrutado automáticamente otro centro de datos.
 *  Para *escribe*, planeada Hola directory will conmutación por error (maestro) réplica principal en centros de datos a través de (nuevo elemento principal es sincronizado tooold principal) o procedimientos de emergencia de conmutación por error. Durabilidad de los datos se consigue mediante la replicación de los centros de datos de tooat dos mínimos de confirmación.

**Coherencia de datos**

modelo de directorio de Hello es uno de coherencia definitiva. Uno de los problemas típico con los sistemas distribuidos de replicación de forma asincrónica es que datos de hello devueltos desde una réplica "determinada" no pueden ser up toodate. 

Azure AD proporciona coherencia de lectura y escritura para las aplicaciones dirigidas a una réplica secundaria al enrutar su réplica principal de escrituras toohello y sincrónicamente extrayendo Hola vuelve a escribir toohello de réplica secundaria.

Aplicación escribe mediante Hola Graph API de Azure AD se extraen de mantenimiento de réplica de directorio tooa de afinidad para la coherencia de lectura y escritura. servicio de Azure AD Graph Hola mantiene una sesión lógica, que tiene afinidad tooa réplica secundaria usa para las lecturas; la afinidad se captura en un token de réplica"" que Hola memorias caché de servicio de gráfico con una memoria caché distribuida. Este token, a continuación, se utiliza para las operaciones posteriores de hello misma sesión lógica. 

 >[!NOTE]
 >Escribe inmediatamente se replica se emitieron lecturas toohello réplica secundaria toowhich Hola lógico de la sesión.
 >

**Protección de copia de seguridad**

directorio de Hello implementa eliminaciones suaves, en lugar de eliminaciones de disco duras, para los usuarios y los inquilinos para la recuperación fácil en el caso de eliminaciones accidentales por un cliente. Si el Administrador de inquilinos accidentalmente elimina los usuarios, pueden deshacer fácilmente y restaurar los usuarios de hello eliminado. 

Azure AD implementa copias de seguridad diarias de todos los datos y, por tanto, puede restaurar de forma autoritativa los datos en el caso de eliminaciones lógicas o daños. Nuestro nivel de datos emplea códigos de corrección de errores, por lo que se puede comprobar si hay errores y corregir automáticamente determinados tipos de errores de disco.

**Métricas y supervisiones**

Ejecutar un servicio de alta disponibilidad requiere métricas y funcionalidades de supervisión de primer nivel. Azure AD analiza continuamente e informa de métricas de estado de servicio clave y de criterios de éxito para cada uno de sus servicios. Continuamente desarrollamos y optimizamos métricas, capacidades de supervisión y de alerta para cada escenario, dentro de cada servicio de Azure AD y en todos los servicios.

Si cualquier servicio de Azure AD no funciona según lo esperado, inmediatamente tomamos la funcionalidad de toorestore acción tan pronto como sea posible. Hola pistas de Azure AD de la métrica más importantes es rapidez podemos detectar y mitigar un cliente o live problema de sitio. Se trata de invertir en gran medida de supervisión y alertas toominimize tiempo toodetect (destino TTD: < 5 minutos) y preparación operativa toominimize tiempo toomitigate (últimos doce meses destino: < 30 minutos).

**Operaciones seguras**

Empleamos controles operativos, como Multi-Factor Authentication (MFA) para cualquier operación, así como la auditoría de todas las operaciones. Además, usamos un elevación de just-in-time sistema toogrant temporal acceso necesario para cualquier operativa tarea a petición de forma continuada. Para obtener más información, consulte [Hola de confianza en la nube](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Pasos siguientes
[Guía del desarrollador de Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)


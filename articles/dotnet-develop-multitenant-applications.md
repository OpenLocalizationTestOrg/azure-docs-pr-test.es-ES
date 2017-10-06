---
title: "Patrón de aplicación Web de inquilino aaaMulti | Documentos de Microsoft"
description: "Encuentre información general de arquitectura y patrones de diseño que describen cómo tooimplement de varios inquilinos web aplicación en Azure."
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Aplicaciones multiempresa en Azure
Una aplicación para varios inquilinos es un recurso compartido que permite tooview independientes sobre los usuarios, o "inquilinos," hello aplicación como si fuese su propios. Un escenario típico que se presta tooa de aplicación para varios inquilinos es uno en las que todos los usuarios de hello aplicación puede desea la experiencia del usuario de hello toocustomize pero en caso contrario Hola los mismos requisitos empresariales básicos. Office 365, Outlook.com y visualstudio.com son ejemplos de grandes aplicaciones multiempresa.

Desde la perspectiva del proveedor de la aplicación, ventajas de saludo de la arquitectura multiempresa principalmente relacionan toooperational y una reducción de costes. Una versión de la aplicación puede satisfacer las necesidades de Hola de muchos inquilinos/customers, lo que permite la consolidación del sistema de las tareas de administración, como supervisión, ajuste del rendimiento, mantenimiento de software y las copias de seguridad de datos.

siguiente Hola proporciona una lista de los objetivos más importantes de Hola y requisitos desde la perspectiva de un proveedor de servicios.

* **Aprovisionamiento**: debe ser capaz de tooprovision nuevos inquilinos para la aplicación hello.  Aplicaciones para varios inquilinos con un gran número de los inquilinos, es tooautomate suele ser necesario hacerlo por habilitar el aprovisionamiento de autoservicio.
* **Mantenimiento**: debe ser capaz de tooupgrade Hola aplicación y realizar otras tareas de mantenimiento mientras lo están usando varios inquilinos.
* **Supervisión**: se debe ser capaz de toomonitor aplicación de hello en todo momento tooidentify los problemas y tootroubleshoot ellos. Esto incluye la supervisión cómo cada inquilino está usando la aplicación hello.

Una aplicación para varios inquilinos implementada correctamente proporciona siguiente Hola beneficia toousers.

* **Aislamiento**: actividades de Hola de inquilinos individuales no afectan al uso de Hola de aplicación hello otros inquilinos de. Los inquilinos no pueden tener acceso a los datos de los demás. Parece toohello inquilino como si tuvieran el uso exclusivo de aplicación hello.
* **Disponibilidad**: parte de inquilinos individuales desea toobe de aplicación Hola constantemente disponible, quizás con garantías definidas en un SLA. Nuevo, actividades Hola de otros inquilinos no deberían afectar a la disponibilidad de Hola de aplicación hello.
* **Escalabilidad**: aplicación Hola adapta a petición de hello toomeet de inquilinos individuales. Hello presencia y las acciones de otros inquilinos no deberían afectar al rendimiento de Hola de aplicación hello.
* **Los costos de**: los costos son menores que ejecutan una aplicación dedicada, único inquilino porque la arquitectura multiempresa permite Hola uso compartido de recursos.
* **Personalización**. aplicación de Hello capacidad toocustomize Hola para un inquilino individual de varias maneras, como agregar o quitar características, cambiar colores y logotipos o incluso agregar su propio código o script.

En resumen, aunque hay muchas consideraciones que debe tener en cuenta tooprovide un servicio altamente escalable, también hay una serie de objetivos de Hola y requisitos de aplicaciones para varios inquilinos de toomany comunes. Algunos pueden no ser relevante en escenarios específicos y la importancia de Hola de objetivos individuales y requisitos serán diferentes en cada escenario. Como proveedor de la aplicación para varios inquilinos de hello, también tendrá objetivos y requisitos como, cumpliendo los inquilinos de hello objetivos y requisitos, rentabilidad, facturación, varios niveles de servicio, aprovisionamiento, mantenimiento de supervisión y automatización.

Para obtener más información acerca de consideraciones de diseño adicionales de una aplicación multiinquilino, consulte [Hospedaje de una aplicación multiinquilino en Azure][Hosting a Multi-Tenant Application on Azure]. Para obtener información sobre los patrones comunes de la arquitectura de datos de aplicaciones de base de datos de software como servicio (SaaS) multiinquilino, consulte [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

Azure proporciona muchas características que le permiten tooaddress Hola problemas claves que se producen al diseñar un sistema para varios inquilinos.

**Aislamiento**

* Segmentación de inquilinos de sitios web mediante encabezados host con o sin comunicación de SSL
* Segmentar inquilinos de sitio web según parámetros de consulta
* Servicios web en roles de trabajo
  * Roles de trabajo por lo general que procesan los datos en hello back-end de una aplicación.
  * Roles de Web que normalmente actúan como Hola front-end para las aplicaciones.

**Almacenamiento**

Administración de datos como los servicios de almacenamiento de Azure o base de datos de SQL Azure como Hola tabla servicio que proporciona servicios de almacenamiento de grandes cantidades de datos no estructurados y Hola servicio Blob que proporciona servicios toostore grandes cantidades de texto no estructurado o datos binarios, como vídeo, audio e imágenes.

* Proteger los datos multiempresa en la Base de datos SQL apropiada para inicios de sesión de SQL Server por inquilino.
* Uso de tablas de Azure para aplicación de recursos mediante la especificación de una directiva de acceso de nivel de contenedor, puede Hola permisos tooadjust de capacidad sin necesidad de tooissue direcciones URL nuevas para los recursos de hello protegidos con firmas de acceso compartido.
* Las colas de Azure para las colas de recursos de aplicaciones de Azure son toodrive utilizada en nombre de inquilinos de procesamiento, pero también puede ser usado toodistribute trabajo necesario para el aprovisionamiento y administración.
* Colas de Bus de servicio para recursos de la aplicación que tooa de trabajo inserta un servicio compartido, puede usar una cola única donde cada remitente del inquilino solo tiene cola de toothat toopush permisos (según se derive de las notificaciones emitidas desde ACS), mientras solo destinatarios de hello del servicio de Hola tener permiso toopull de datos de Hola de cola de Hola procedentes de varios inquilinos.

**Servicios de conexión y seguridad**

* Service Bus de Azure, una infraestructura de mensajería que se ubica entre aplicaciones permitiéndoles tooexchange mensajes de una manera de acoplamiento flexible para escalabilidad mejorada y resistencia.

**Servicios de red**

Azure ofrece varios servicios de red que admiten la autenticación y mejoran la manejabilidad de las aplicaciones hospedadas. Estos servicios Hola siguientes:

* La Red virtual de Azure le permite aprovisionar y administrar redes privadas virtuales (VPN) en Azure, así como vincularlas de forma segura con la infraestructura de TI local.
* Administrador de tráfico de red virtual le permite equilibrar tooload el tráfico entrante a través de Azure hospedado varios servicios si se está ejecutando en hello mismo centro de datos o entre distintos centros de datos alrededor de Hola a todos.
* Azure Active Directory (Azure AD) es un servicio moderno basado en REST que ofrece capacidades de administración de identidades y control de acceso para las aplicaciones en la nube. Con Azure AD para recursos de la aplicación Azure AD tooprovides una manera sencilla de autenticar y autorizar a los usuarios toogain acceso tooyour aplicaciones y servicios web al que permite que las características de Hola de autenticación y autorización toobe factorizado fuera de su código.
* El Bus de servicio de Azure ofrece una capacidad de flujo de datos y mensajería segura para aplicaciones distribuidas e híbridas, como la comunicación entre aplicaciones hospedadas de Azure y aplicaciones y servicios locales, sin requerir infraestructuras de seguridad y firewall complejas. Con Service Bus Relay para toohello de recursos de la aplicación de servicios que se exponen como extremos pueden pertenecer toohello inquilinos (por ejemplo, hospedado fuera de sistema de hello, como local) o pueden ser servicios aprovisionados específicamente para (inquilino) Hola Dado que los datos confidenciales, específicos del inquilino se pasan a través de ellos).

**Aprovisionamiento de recursos**

Azure proporciona a varias maneras de nuevos inquilinos de aprovisionamiento para la aplicación hello. Aplicaciones para varios inquilinos con un gran número de los inquilinos, es tooautomate suele ser necesario hacerlo por habilitar el aprovisionamiento de autoservicio.

* Roles de trabajo permite tooprovision y eliminación aprovisionar recursos por inquilino (por ejemplo, cuando un nuevo inquilino registra o cancela), recopilar métricas para medición de usar y administrar el escalado de una programación específica o en respuesta toohello haber superado los umbrales de clave indicadores de rendimiento. Este mismo rol también puede ser utilizado toopush horizontal de las actualizaciones de solución toohello.
* Blobs de Azure pueden ser usado tooprovision compute o recursos de almacenamiento ya inicializado para nuevos inquilinos proporcionando contenedor acceso a las directivas tooprotect Hola proceso paquetes de servicios, imágenes VHD y otros recursos.
* Las opciones para aprovisionar los recursos de la Base de datos SQL para un inquilino incluyen:
  
  * DDL en scripts o insertados como recursos en ensamblados
  * Paquetes SQL Server 2008 R2 DAC implementados mediante programación
  * Copiar desde una base de datos de referencia maestra
  * Usa la base de datos de importación y exportación tooprovision nuevas bases de datos desde un archivo.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716

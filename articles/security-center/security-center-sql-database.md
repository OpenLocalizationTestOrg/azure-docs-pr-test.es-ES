---
title: aaaAzure servicio Centro de seguridad y la base de datos de SQL de Azure | Documentos de Microsoft
description: "En este artículo se explica cómo Security Center puede ayudarle a proteger bases de datos en Azure SQL Database."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Servicios Azure Security Center y Azure SQL Database
[Centro de seguridad de Azure](https://azure.microsoft.com/documentation/services/security-center/) le ayuda a evitar, detectar y responder toothreats. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

En este artículo se explica cómo Security Center puede ayudarlo a proteger bases de datos en Azure SQL Database.

## <a name="why-use-security-center"></a>Razones para usar Security Center
Centro de seguridad ayuda a proteger los datos en la base de datos SQL proporcionando visibilidad sobre seguridad Hola de todos los servidores y bases de datos. Con Security Center puede realizar estas tareas:

* Definir las directivas de auditoría y cifrado de SQL Database
* Supervisión de seguridad de Hola de recursos de base de datos SQL en todas sus suscripciones.
* Identificar y corregir problemas de seguridad rápidamente
* Integrar las alertas de [detección de amenazas de Azure SQL Database](../sql-database/sql-database-threat-detection.md)

Además toohelping proteger los recursos de base de datos SQL, centro de seguridad también proporciona supervisión de la seguridad y la administración de máquinas virtuales de Azure, servicios en la nube, servicios de aplicaciones, redes virtuales y mucho más. Obtenga más información sobre Security Center [aquí](security-center-intro.md).

## <a name="prerequisites"></a>Requisitos previos
tooget a trabajar con el centro de seguridad, debe tener un tooMicrosoft de suscripción a Azure. nivel gratis de Hello del centro de seguridad está habilitada con su suscripción. Para obtener más información sobre los niveles Gratis y Estándar de Security Center, consulte [Centro de seguridad Precios](https://azure.microsoft.com/pricing/details/security-center/).

El Centro de seguridad admite el acceso basado en rol. toolearn más información acerca de control de acceso basado en roles (RBAC) en Azure, consulte [basada en roles de Azure Active Directory Access Control](../active-directory/role-based-access-control-configure.md). Hello p+f acerca del centro de seguridad se proporciona información sobre [cómo se administran los permisos en el centro de seguridad](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Acceso al Centro de seguridad
Acceder a centro de seguridad de hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/). [Inicie sesión en el portal de toohello](https://portal.azure.com/) y seleccione hello **opción de centro de seguridad**.

![Opción de Security Center][1]

Hola **centro de seguridad** abre la hoja.
![Hoja Security Center][2]

## <a name="set-security-policy"></a>Establecimiento de directivas de seguridad
Una directiva de seguridad define Hola conjunto de controles que se recomiendan para los recursos dentro de hello especificado suscripción o grupo de recursos. En el centro de seguridad, definir directivas para sus suscripciones o grupos de recursos según tooyour las necesidades de seguridad y empresa tipo hello de aplicaciones o importancia de los datos de hello en cada suscripción.

Puede establecer una directiva tooshow recomendaciones para la auditoría de SQL y el cifrado de datos transparente (TDE) de SQL.

* Al activar **detección de amenazas y auditoría de SQL**, centro de seguridad se recomienda que la auditoría de acceso tooAzure base de datos esté habilitado para el cumplimiento, detección y con fines de investigación avanzadas.
* Al activar el **cifrado de datos transparente de SQL**, Security Center recomienda que el cifrado en reposo se habilite para Azure SQL Database, las copias de seguridad asociadas y los archivos de registro de transacciones.

tooset una directiva de seguridad, seleccione hello **directiva** icono hoja de centro de seguridad de Hola. En hello **directiva de seguridad** hoja, suscripción seleccione Hola que servirá de directiva de seguridad de tooenable Hola. Seleccione **directivas de prevención** y activar **en** Hola recomendaciones de seguridad que desea toouse en esta suscripción.
![Directiva de seguridad][3]

más información, consulte toolearn [establecer directivas de seguridad](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Administración de recomendaciones de seguridad
Centro de seguridad periódicamente analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el Centro de seguridad identifica vulnerabilidades de seguridad potenciales, crea recomendaciones. recomendaciones de Hello guiarle por proceso de Hola de configuración de controles de Hola que sea necesitado.

Después de establecer una directiva de seguridad, el centro de seguridad analiza el estado de seguridad de Hola de sus tooidentify posibles vulnerabilidades de recursos. recomendaciones de Hola se muestran en un formato de tabla, donde cada línea representa una recomendación concreta. Usar hello en la tabla siguiente como un toohelp de referencia que comprende recomendaciones disponibles de Hola para base de datos de SQL Azure, y qué cada recomendación no si se aplica. Al seleccionar una recomendación le tooan artículo que explica cómo tooimplement Hola recomendación en el centro de seguridad.

| Recomendación | Description |
| --- | --- |
| [Habilitar la auditoría y la detección de amenazas en los servidores SQL](security-center-enable-auditing-on-sql-servers.md) |Recomienda activar la detección de amenazas y la auditoría en los servidores de SQL Database. (Solo disponible para el servicio SQL Database. Se excluyen las instancias de Microsoft SQL Server que se ejecutan en las máquinas virtuales). |
| [Habilitar la auditoría y la detección de amenazas en las bases de datos SQL](security-center-enable-auditing-on-sql-databases.md) |Recomienda activar la detección de amenazas y la auditoría en las bases de datos de SQL Database. (Solo disponible para el servicio SQL Database. Se excluyen las instancias de Microsoft SQL Server que se ejecutan en las máquinas virtuales). |
| [Habilitar el cifrado de datos transparente](security-center-enable-transparent-data-encryption.md) |Recomienda habilitar el cifrado en las bases de datos SQL (solo disponible para el servicio SQL Database). |

recomendaciones de toosee para los recursos de Azure, seleccione hello **recomendaciones** icono hoja de centro de seguridad de Hola. En hello **recomendaciones** hoja, seleccione un detalles de toosee de recomendación. En este ejemplo, vamos a seleccionar la recomendación de **habilitar la auditoría y la detección de amenazas en los servidores SQL**.

![Recomendaciones][4]

Como se muestra a continuación, se muestra en el centro de seguridad Hola donde no están habilitadas la detección de amenazas y auditoría de servidores de SQL Server. Después de activar la auditoría, puede configurar opciones de detección de amenazas y alertas de correo electrónico tooreceive de configuración de la seguridad. La detección de amenazas le avisa cuando detecte actividades anómalas de la base de datos que indican la base de datos toohello amenazas de seguridad potenciales. Hola alertas se muestran en el panel del centro de seguridad de Hola.
![Detección de amenazas y auditoría][5]

Siga los pasos de hello en [detección de amenazas de base de datos SQL en el portal de Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn en y configurar la detección de amenazas y lista de hello tooconfigure de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas.

toolearn más información acerca de las recomendaciones, consulte [administrar las recomendaciones de seguridad](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Supervisión del estado de la seguridad
Después de habilitar [las directivas de seguridad](security-center-policies.md) para obtener recursos de una suscripción, el centro de seguridad analizará seguridad Hola de sus tooidentify posibles vulnerabilidades de recursos.  Puede ver estado de los recursos de seguridad de Hola Hola **estado de seguridad del recurso** icono. Al hacer clic en **datos** en hello **estado de seguridad del recurso** icono, hello **los recursos de datos** hoja se abre con las recomendaciones de SQL para problemas como la auditoría y transparente no está habilitado el cifrado de datos. También tiene las recomendaciones para el estado de mantenimiento general de Hola de base de datos de Hola.
![Estado de seguridad de los recursos][6]

más información, consulte toolearn [supervisión de estado de seguridad](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Administrar y responder a alertas de toosecurity
Centro de seguridad automáticamente recopila, analiza y se integra datos de registro de [detección de amenazas de SQL Azure](../sql-database/sql-database-threat-detection.md), así como otros recursos de Azure, toodetect reales amenazas y reducir los falsos positivos. Se muestra una lista de alertas de seguridad con prioridades en el centro de seguridad junto con hello información que necesita tooquickly investigar el problema de Hola y recomendaciones sobre cómo tooremediate un ataque.

toosee alertas, seleccione hello **alertas de seguridad** icono hoja de centro de seguridad de Hola. En hello **alertas de seguridad** hoja, seleccione una alerta toolearn más información acerca de los eventos de Hola que desencadenó la alerta de Hola y qué, si existe, los pasos necesita tootake tooremediate un ataque. En este ejemplo, vamos a seleccionar el **posible ataque por inyección de código SQL**.
![Alertas de seguridad][7]

Tal y como se muestra a continuación, el centro de seguridad proporciona detalles adicionales que ofrecen una visión general de qué alerta desencadenada hello, hello recurso, de destino cuando Hola procede del origen de dirección IP y recomendaciones sobre cómo tooremediate.
![Posible ataque por inyección de código SQL][8]

más información, consulte toolearn [responde y administrar alertas de toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes del centro de seguridad](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Guía de planeación y las operaciones de centro de seguridad](security-center-planning-and-operations-guide.md) : seguir un conjunto de pasos y tareas toooptimize el uso del centro de seguridad en función de los requisitos de seguridad y el modelo de administración de nube de su organización.
* [Seguridad de datos de Security Center](security-center-data-security.md): obtenga información sobre cómo Security Center recopila y procesa datos de los recursos de Azure, entre los que se incluyen la información de configuración, los metadatos, los registros de eventos y los archivos de volcado de memoria, entre otros.
* [Control de incidentes de seguridad](security-center-incident.md) -Obtenga información acerca de la seguridad de hello toouse alerta capacidad en el centro de seguridad tooassist en control de incidentes de seguridad.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png

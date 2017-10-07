---
title: "administración de aaaService para la búsqueda de Azure en hello portal de Azure"
description: "Administrar búsqueda de Azure, un servicio de búsqueda de nube hospedada en Microsoft Azure, mediante Hola portal de Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Administración del servicio de búsqueda de Azure en hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Azure Search es un servicio basado en la nube totalmente administrado que se utiliza para la creación de una experiencia de búsqueda enriquecida en aplicaciones personalizadas. Este artículo tratan hello *la administración del servicio* tareas que puede realizar en hello [portal de Azure](https://portal.azure.com) para un servicio de búsqueda que ya haya aprovisionado. *La administración del servicio* es ligero de forma predeterminada, toohello limitado después de tareas:

* Administrar y proteger el acceso toohello *claves de api* utilizado para servicio de tooyour de acceso de lectura o escritura.
* Ajustar la capacidad del servicio cambiando la asignación de Hola de particiones y réplicas.
* Supervisar el uso de recursos, toomaximum relativa límites de su nivel de servicio.

**Fuera del ámbito** 

*Administración de contenido* (o administración de índice) hace referencia toooperations como análisis de volumen de consulta de búsqueda tráfico toounderstand, detectar los términos que personas buscar y búsqueda éxito resultados están en guiar a los clientes toospecific documentos en el índice. Para obtener ayuda en esta área, visite [Análisis de tráfico de búsqueda para Azure Search](search-traffic-analytics.md).

*Rendimiento de las consultas* también está más allá del ámbito de Hola de este artículo. Para más información, vea [Supervisar el uso y las métricas de consultas](search-monitor-usage.md) y [Rendimiento y optimización](search-performance-optimization.md).

La *actualización* no es una tarea administrativa. Dado que se asignan los recursos cuando se aprovisiona el servicio de hello, móvil tooa a otro nivel requiere un nuevo servicio. Consulte [Creación de un servicio Azure Search](search-create-service-portal.md) para más información.

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Derechos de administrador
El aprovisionamiento o retirar el propio servicio Hola puede realizarse por un administrador de suscripción de Azure o Coadministrador.

Dentro de un servicio, cualquier persona con la dirección URL del servicio de acceso toohello y una clave de api de administración tiene acceso de lectura y escritura toohello servicio. Acceso de lectura y escritura proporciona tooadd de capacidad de hello, eliminar o modificar objetos de servidor, incluidos claves de api, índices, los indizadores, orígenes de datos, programaciones y las asignaciones de roles, tal y como se implementa a través de [roles definidos por el RBAC](#rbac).

Todas las interacciones de usuario con búsqueda de Azure se encuentra dentro de uno de estos modos: lectura y escritura acceso toohello servicio (derechos de administrador) o servicio de toohello de acceso de solo lectura (derechos de consulta). Para obtener más información, consulte [administrar claves de api de hello](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>Configuración de roles RBAC para el acceso administrativo
Azure proporciona un [modelo de autorización basada en funciones globales](../active-directory/role-based-access-control-configure.md) para todos los servicios que se administran a través del portal de Hola o las API del Administrador de recursos. Roles de propietario, Colaborador y lector determinan nivel Hola de administración de servicio de rol de tooeach asignado de entidades de seguridad, grupos y usuarios de Active Directory. 

Búsqueda de Azure, los permisos de RBAC determinan Hola después de las tareas administrativas:

| Rol | Tarea |
| --- | --- |
| Propietario |Crear o eliminar el servicio de Hola o cualquier objeto de servicio de hello, incluidas las claves de api, índices, los indizadores, orígenes de datos de indizador y programaciones de indizador.<p>Ver el estado del servicio, incluidos el tamaño de almacenamiento y los recuentos.<p>Agregar o eliminar miembros del rol (solo un propietario puede administrar la pertenencia a roles).<p>Los administradores de suscripciones y los propietarios de servicio tienen pertenencia automática en función de los propietarios de Hola. |
| Colaborador |El mismo nivel de acceso que Propietario, menos el administración de roles RBAC. Por ejemplo, un usuario con el rol Colaborador puede ver y regenerar `api-key`, pero no puede modificar pertenencias a roles. |
| Lector |Ver las claves de estado y consulta de servicio. Los miembros de este rol no pueden cambiar la configuración de un servicio, ni pueden ver claves de administrador. |

Funciones no conceden a extremo de servicio de toohello de derechos de acceso. Las operaciones del servicio de búsqueda, como la administración de índices, el rellenado del índice y las consultas en datos de búsqueda, se controlan mediante claves de API, no a través de roles. Para más información, consulte "Autorización para administración frente a operaciones de datos" en [¿Qué es el control de acceso basado en roles?](../active-directory/role-based-access-control-what-is.md)

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Registro e información del sistema
Búsqueda de Azure no exponer los archivos de registro para un servicio concreto, ya sea a través del portal de Hola o interfaces de programación. En el nivel básico de Hola y versiones posteriores, Microsoft supervisa todos los servicios de búsqueda de Azure para disponibilidad del 99,9% por los contratos de nivel de servicio (SLA). Si el servicio de hello es lento o rendimiento de la solicitud está por debajo de los umbrales de SLA, los equipos de soporte técnico revisión toothem disponible de archivos de registro de hello y problema de Hola de dirección.

En términos de información general sobre el servicio, puede obtener información de hello siguientes maneras:

* En el portal hello, en panel de servicio de hello, a través de las notificaciones, las propiedades y mensajes de estado.
* Usar [PowerShell](search-manage-powershell.md) o hello [API de REST de administración](https://docs.microsoft.com/rest/api/searchmanagement/) demasiado[obtener propiedades del servicio](https://docs.microsoft.com/rest/api/searchmanagement/services), o el estado en el uso de recursos de índice.
* A través del [análisis de tráfico de búsqueda](search-traffic-analytics.md), como se ha indicado anteriormente.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>Administración de las claves de API
Todas las solicitudes de servicio de búsqueda de tooa necesita una clave de api que se generó específicamente para su servicio. Esta clave de api es único mecanismo de Hola para autenticar el extremo de servicio de búsqueda de tooyour de acceso. 

Una clave de API es una cadena que se compone de letras y números generados aleatoriamente. A través de [permisos RBAC](#rbac), puede eliminar o leer Hola claves, pero no se puede reemplazar una clave con una contraseña definida por el usuario. 

Dos tipos de claves son tooaccess usa el servicio de búsqueda:

* Administración (válido para cualquier operación de lectura y escritura en el servicio de hello)
* Consulta (válida para operaciones de solo lectura, como las consultas en un índice)

Cuando se aprovisiona el servicio de hello, se crea una clave de api de administración. Hay dos claves de administración, designadas como *principal* y *secundaria* tookeep ellas directamente, pero en realidad son intercambiables. Cada servicio tiene dos claves de administración para que pueda poner uno sin perder acceso tooyour servicio. Puede volver a generar la clave administrador, pero no se puede agregar toohello recuento de claves de administrador total. Hay un máximo de dos claves de administración por servicio de búsqueda.

Las claves de consulta están diseñadas para las aplicaciones cliente que llaman directamente a Azure Search. Puede crear las claves de consulta too50. En código de aplicación, puede especificar dirección URL de búsqueda de Hola y un servicio de toohello de acceso de solo lectura de tooallow clave de api de consulta. El código de aplicación también especifica el índice de hello utilizado por la aplicación. Juntos, punto de conexión de hello, una clave de api para el acceso de solo lectura y un índice de destino definen Hola ámbito y nivel de acceso de conexión de Hola desde la aplicación cliente.

tooget o regenerar claves de api, panel de servicio de hello abierto. Haga clic en **claves** tooslide abrir la página de administración de claves de Hola. Comandos para volver a generar o para crear claves están al principio de Hola de página de Hola. De forma predeterminada, solo se crean claves de administración. Las claves de API de consulta deben crearse manualmente.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Protección de las claves de API
Clave de seguridad está garantizada restringiendo el acceso a través del portal de Hola o interfaces de administrador de recursos (interfaz de línea de comandos o PowerShell). Como se ha indicado, los administradores de suscripciones pueden ver y volver a generar todas las claves de API. Como medida de precaución, consulte toounderstand de asignaciones de rol que tenga claves de administración de acceso toohello.

1. En el panel de servicio de hello, haga clic en hoja de usuarios de hello acceso icono tooslide Hola abierto.
   ![][7]
2. En Usuarios, revise las asignaciones de roles existentes. Según lo esperado, los administradores de suscripciones ya tienen el servicio de toohello de acceso completo a través del rol de propietario de Hola.
3. toodrill aún más, haga clic en **los administradores de suscripciones** y, a continuación, expanda hello toosee de lista de asignación de rol que tenga derechos de administración compartida en el servicio de búsqueda.

Permisos de acceso de otra manera tooview es tooclick **Roles** en la hoja de usuarios de Hola. Si lo hace, muestra roles disponibles y el número de Hola de rol tooeach asignado a los usuarios o grupos.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>Supervisar el uso de recursos
En el panel de hello, supervisión de recursos es información toohello limitada que se muestra en el panel de servicio de Hola y algunas métricas que puede obtener mediante una consulta de servicio de Hola. En el panel de servicio de hello, en la sección uso hello, puede determinar rápidamente si los niveles de recursos de partición sean las adecuadas para su aplicación.

Con hello API del servicio de búsqueda, puede obtener un recuento en documentos y los índices. Hay límites estrictos asociados con estos recuentos basados en hello nivel de precios. Para más información, consulte [Límites de servicio en Azure Search](search-limits-quotas-capacity.md). 

* [Obtención de estadísticas de índice](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Recuento de documentos](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Los comportamientos de Almacenamiento en caché pueden sobrevalorar un límite temporalmente. Por ejemplo, cuando se usa el servicio de hello compartido, puede ver un documento recuento por encima del límite de disco duro de Hola de 10.000 documentos. sobrevaloración Hello es temporal y se detectarán en la siguiente comprobación de límite Hola. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Interrupciones de servicio y recuperación ante desastres

Aunque nos podemos recuperar los datos, búsqueda de Azure no proporciona la conmutación por error instantánea del servicio de hello si hay una interrupción en el nivel del centro de datos o clúster de Hola. Si se produce un error en un clúster en el centro de datos de Hola, equipo de operaciones de hello detectará y servicio de toorestore de trabajo. Experimentará un tiempo de inactividad durante la restauración del servicio. Puede solicitar servicio créditos toocompensate de no disponibilidad del servicio por hello [contrato de nivel de servicio (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Si continua del servicio es necesario en caso de hello de errores catastróficos fuera de control de Microsoft, se puede realizar [aprovisionar un servicio adicional](search-create-service-portal.md) en una región distinta e implemente una replicación geográfica estrategia tooensure índices son totalmente redundantes en todos los servicios.

Los clientes que usen [indizadores](search-indexer-overview.md) toopopulate y la actualización de índices pueden controlar la recuperación ante desastres mediante indizadores geográfica específica aprovechando Hola mismo origen de datos. Dos servicios en regiones diferentes, cada uno ejecuta un indizador, pudieron indizar de hello mismo tooachieve redundancia geográfica del origen de datos. Si indexa desde orígenes de datos que también tienen redundancia geográfica, tenga en cuenta que los indizadores de Azure Search solo pueden realizar una indización incremental a partir de las réplicas principales. En un evento de conmutación por error, ser seguro toore punto Hola indizador toohello nueva réplica principal. 

Si no utiliza los indizadores, usaría los código toopush objetos y datos toodifferent buscar servicios de aplicaciones en paralelo. Para más información, consulte [Consideraciones sobre el rendimiento y la optimización de Azure Search](search-performance-optimization.md).

## <a name="backup-and-restore"></a>Copia de seguridad y restauración

Dado que Azure Search no es una solución de almacenamiento de datos principal, no se proporcionan un mecanismo formal para realizar procesos de copias de seguridad y restauración automáticos. El código de aplicación que se usa para crear y rellenar un índice es Hola de hecho opción de restauración si elimina por error un índice. 

toorebuild un índice, elimínelo (si existe), vuelva a crear índice hello en el servicio de Hola y volver a cargar mediante la recuperación de datos del almacén de datos principal. Como alternativa, puede llegar a demasiado[soporte al cliente]() toosalvage índices si se produce una interrupción regional del sistema.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Escalado o reducción vertical
Cada uno de los servicios de búsqueda se inicia con una cantidad mínima de una réplica y una partición. Si ha iniciado sesión en un [nivel que proporciona recursos dedicados](search-limits-quotas-capacity.md), haga clic en hello **escala** icono Hola servicio panel tooadjust uso de recursos.

Cuando se agrega capacidad a través de cualquier recurso, el servicio de hello ellos utiliza de forma automática. No es necesario realizar ninguna otra acción por su parte, pero no hay un breve lapso de tiempo antes de que se percibe el impacto de Hola de nuevo recurso de Hola. Puede tardar 15 minutos o más tooprovision recursos adicionales.

 ![][10]

### <a name="add-replicas"></a>Adición de réplicas
La adición de réplicas permiten un aumento de las consultas por segundo (QPS) o la consecución de una alta disponibilidad. Cada réplica tiene una copia de un índice, por lo que agregar una réplica más traduce tooone más índice disponible para controlar las solicitudes de consulta de servicio. Para lograr una alta disponibilidad, se requieren un mínimo de tres réplicas (para más información, consulte [Escalado de niveles de recursos para cargas de trabajo de indexación y consulta en Azure Search](search-capacity-planning.md) ).

Un servicio de búsqueda con más réplicas puede equilibrar la carga de solicitudes de consulta sobre un número de índices mayor. Proporciona un nivel de volumen de la consulta, rendimiento de la consulta va toobe más rápidamente cuando hay más copias de solicitud de hello índice disponible tooservice Hola. Si experimenta una latencia de las consultas, puede esperar un impacto positivo sobre el rendimiento cuando réplicas adicionales de hello están en línea.

Aunque el rendimiento de la consulta aumenta a medida que agregue las réplicas, no con precisión doble o triple a medida que agregue el servicio de tooyour de réplicas. Todas las aplicaciones de búsqueda son factores de tooexternal de asunto que pueden afectar al rendimiento de la consulta. Las consultas más complejas y latencia de red son dos factores que contribuyen toovariations en los tiempos de respuesta de consultas.

### <a name="add-partitions"></a>Adición de particiones
La mayoría de las aplicaciones de servicio tienen una necesidad integrada de más réplicas, en lugar de particiones. En los casos donde se requiere un mayor número de documentos, puede agregar particiones si se registró en un servicio Estándar. El nivel Básico no proporciona particiones adicionales.

En el nivel de estándar de hello, se agregan particiones en múltiplos de 12 (específicamente, 1, 2, 3, 4, 6 o 12). Se trata de un artefacto de particionamiento. Un índice se crea en 12 particiones de base de datos, que pueden almacenarse en su totalidad en una partición o dividirse equitativamente en 2, 3, 4, 6 o 12 particiones (una partición de base de datos por partición).

### <a name="remove-replicas"></a>Eliminación de réplicas
Tras períodos de elevados volúmenes de consultas, puede reducir las réplicas después de que se hayan normalizado las cargas de consultas de búsqueda (por ejemplo, tras finalizar las ventas navideñas).

toodo, mover Hola réplica control deslizante tooa atrás número menor. No es necesario que haga nada más. Reducir el número de réplicas de hello cede máquinas virtuales en el centro de datos de Hola. Ahora, sus operaciones de ingesta de consultas y datos se ejecutarán en menos VM que antes. límite mínimo de Hello es una réplica.

### <a name="remove-partitions"></a>Eliminación de particiones
A diferencia de quitar las réplicas, que no requiere ningún esfuerzo adicional por su parte, puede que tenga algunas toodo de trabajo si utiliza más espacio de almacenamiento que se puede reducir. Por ejemplo, si la solución utiliza tres particiones, la reducción tooone o dos particiones generará un error si el nuevo espacio de almacenamiento hello es menor que requiere. Como cabría esperar, las opciones son índices toodelete o documentos dentro de un toofree de índice asociado espacio o mantener la configuración actual de Hola.

No existe un método de detección que indique qué particiones de índice se almacenan en particiones concretas. Cada partición proporciona aproximadamente 25 GB de almacenamiento, por lo que deberá tamaño tooreduce de tooa del almacenamiento que se puede incluir mediante el número de particiones que tiene Hola. Si desea toorevert tooone partición, todas las 12 particiones deberá toofit.

toohelp con una planificación futura, conviene toocheck almacenamiento (con [obtener estadísticas de índice](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee cuánto realmente utilizado. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Prácticas recomendadas de escalado e implementación
En este vídeo de 30 minutos se analizan las prácticas recomendadas para escenarios de implementación avanzada, entre los que se incluyen las cargas de trabajo distribuidas geográficamente. También puede ver [rendimiento y optimización en búsqueda de Azure](search-performance-optimization.md) para páginas de ayuda que Hola portada mismo señala.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Pasos siguientes
Una vez que comprenda los conceptos de hello detrás de administración del servicio, considere el uso de [PowerShell](search-manage-powershell.md) tooautomate tareas.

También se recomienda revisar hello [rendimiento y optimización de artículo](search-performance-optimization.md).

Otra recomendación es vídeo toowatch Hola se indica en la sección anterior de Hola. Proporciona cobertura más detallada de técnicas de hello mencionados en esta sección.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png




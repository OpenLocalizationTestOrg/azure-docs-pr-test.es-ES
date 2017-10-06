---
title: "Guía de solución de problemas de centro de seguridad aaaAzure | Documentos de Microsoft"
description: Este documento le ayuda a tootroubleshoot problemas en el centro de seguridad de Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Guía de solución de problemas de Azure Security Center
Esta guía es para profesionales de tecnologías de información, los analistas de seguridad de información y los administradores de nube cuyas organizaciones utilizan Azure Security Center y necesitan problemas relacionados con el centro de seguridad de tootroubleshoot.

>[!NOTE] 
>A partir de los principios de junio de 2017, centro de seguridad utiliza Hola Microsoft Monitoring Agent toocollect y almacén de los datos. Vea [migración de la plataforma de Azure Security Center](security-center-platform-migration.md) toolearn más. información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>

## <a name="troubleshooting-guide"></a>Guía de solución de problemas
Esta guía explica cómo problemas relacionados con el centro de seguridad de tootroubleshoot. La mayor parte de la solución de problemas de hello en el centro de seguridad se realiza mirando hello [registro de auditoría](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) registros para hello error de componente. A través de los registros de auditoría puede determinar:

* Qué operaciones se han llevado a cabo
* Quién inició la operación de Hola
* Cuando se ha producido la operación de Hola
* estado de Hola de operación de Hola
* valores de Hello de otras propiedades que pueden ayudarle a investigación operación Hola

registro de auditoría de Hello contiene todas las operaciones de escritura (PUT, POST, DELETE) realizadas en los recursos, sin embargo, no incluye las operaciones de lectura (GET).

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Centro de seguridad usa Hola Microsoft Monitoring Agent: se trata de hello usa el mismo agente por hello Operations Management Suite y el servicio de análisis de registros: toocollect datos de seguridad de máquinas virtuales de Azure. Después de habilita la recopilación de datos y agente Hola está correctamente instalada en el equipo de destino hello, proceso de hello siguiente debe estar en ejecución:

* HealthService.exe

Si abre la consola de administración de servicios (services.msc) de hello, también verá Hola Microsoft Monitoring Agent servicio que se ejecuta tal y como se muestra a continuación:

![Services](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

Abra toosee qué versión del agente de hello tiene, **el Administrador de tareas**, Hola **procesos** pestaña Buscar Hola **servicio del agente de supervisión de Microsoft**, haga doble clic en él y Haga clic en **propiedades**. Hola **detalles** pestaña, examine la versión del archivo hello tal y como se muestra a continuación:

![Archivo](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Escenarios de instalación de Microsoft Monitoring Agent
Hay dos escenarios de instalación que pueden producir resultados diferentes cuando se instala Microsoft Monitoring Agent de hello en el equipo. Hola admitida escenarios son:

* **Agente instalado automáticamente por el centro de seguridad**: en este escenario será capaz de tooview alertas de hello en ubicaciones, el centro de seguridad y búsqueda de registros. Recibirá la dirección de correo electrónico de toohello de notificaciones de correo electrónico que configuró en la directiva de seguridad de Hola para recursos de Hola Hola suscripción pertenece a.
.
* **Agente instalado manualmente en una máquina virtual se encuentra en Azure**: en este escenario, si utiliza agentes descargan e instalarse manualmente anterior tooFebruary 2017, será capaz de tooview alertas de hello en el portal del centro de seguridad de hello solo si se filtra en hello el área de trabajo de suscripción Hola al que pertenece. En caso de filtro en recursos de Hola Hola suscripción pertenece a, no será a toosee capaz de las alertas. Recibirá la dirección de correo electrónico de toohello de notificaciones de correo electrónico que configuró en la directiva de seguridad de hello para el área de trabajo de hello suscripción Hola pertenece a.

>[!NOTE]
> comportamiento de hello tooavoid explicado en hello en segundo lugar, asegúrese de descargar Hola versión más reciente del agente de Hola.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Solución de problemas de los requisitos e red del agente de supervisión
Para agentes tooconnect tooand registrar con el centro de seguridad, deben tener acceso a los recursos toonetwork, incluidos los números de puerto de Hola y direcciones URL de dominio.

- Para los servidores proxy, debe tooensure que Hola recursos se configuran en la configuración del agente de servidor de proxy correspondiente. Lea este artículo para obtener más información en [cómo toochange Hola configuración del proxy](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Para los firewalls que restringen el acceso toohello Internet, deberá tooconfigure el tooOMS de acceso de firewall toopermit. No es necesario realizar ninguna acción en la configuración del agente.

Hello en la tabla siguiente muestra los recursos necesarios para la comunicación.

| Recurso del agente | Puertos | Omitir inspección de HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sí |
| *.oms.opinsights.azure.com | 443 | Sí |
| *.blob.core.windows.net | 443 | Sí |
| *.azure-automation.net | 443 | Sí |

Si encuentra problemas de incorporación con agente hello, asegúrese de artículo de hello tooread seguro [cómo emite la incorporación de Operations Management Suite tootroubleshoot](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>La solución de problemas de Endpoint Protection no funciona correctamente

agente de invitado de Hello es Hola primario proceso todo hello [Microsoft Antimalware](../security/azure-security-antimalware.md) does de extensión. Cuando se produce un error en el proceso del agente invitado hello, Hola Microsoft Antimalware que se ejecuta como un proceso secundario de agente de invitado de hello también puede producir un error.  En escenarios como los se tooverify recomendada Hola siguientes opciones:

- Si Hola destino VM es una imagen personalizada y creador de Hola de hello VM nunca instaló al agente invitado.
- Se producirá un error si el destino de hello es una VM de Linux en lugar de una máquina virtual de Windows, a continuación, instalar versión de Windows hello de extensión de antimalware de hello en una VM de Linux. agente de invitado de Linux de Hello tiene requisitos específicos en cuanto a la versión del sistema operativo y los paquetes necesarios, y si no se cumplen los requisitos de agente de máquina virtual de hello no funcionará no existe o bien. 
- Si Hola máquina virtual se creó con una versión anterior del agente invitado. Si es así, debe tener en cuenta que algunos agentes anterior podrían no actualizaciones automáticas propia versión más reciente de toohello y esto podría provocar problemas de toothis. Utilice siempre la versión más reciente de Hola de agente invitado si crear sus propias imágenes.
- Algunos programas de software de administración de aplicaciones de terceros pueden deshabilitar a agente de invitado de hello, o bloquear el acceso a ubicaciones de archivos de toocertain. Si tiene instalado en su máquina virtual de terceros, asegúrese de que dicho agente Hola está en la lista de exclusión de Hola.
- Ciertos valores de configuración de firewall o el grupo de seguridad de red (NSG) puede bloquear tooand de tráfico de red desde el agente de invitado.
- Cierta lista de control de acceso (ACL) puede impedir el acceso al disco.
- Falta de espacio en disco puede bloquear el agente de invitado de hello funcione correctamente. 

Hola de forma predeterminada está deshabilitada la interfaz de usuario de Antimalware de Microsoft, leer [habilitar la interfaz de usuario de Microsoft Antimalware en Azure Resource Manager máquinas virtuales tras la implementación](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) para obtener más información acerca de cómo tooenable si es necesario.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Solucionar problemas al cargar el panel de Hola

Si experimenta problemas al cargar el panel de centro de seguridad de hello, asegúrese de ese usuario Hola que registra Hola suscripción tooSecurity Center (es decir, Hola primer usuario uno que abrió el centro de seguridad con la suscripción de hello) y usuario de Hola que desearía tooturn en recopilación de datos debe ser *propietario* o *colaborador* de suscripción de Hola. Desde ese momento en también a los usuarios con *lector* en hello suscripción podrá ver Hola panel/alertas/recomendación/directiva.

## <a name="contacting-microsoft-support"></a>Contacto con el soporte técnico de Microsoft
Algunos problemas pueden identificarse mediante el uso de instrucciones de hello proporcionadas en este artículo, otras personas también puede encontrar documentan en public de centro de seguridad de hello [foro](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). Sin embargo, si necesita más información para solucionar el problema, puede abrir una nueva solicitud de soporte técnico mediante **Azure Portal**, como se indica a continuación: 

![Soporte técnico de Microsoft](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo tooconfigure las directivas de seguridad en el centro de seguridad de Azure. toolearn más información acerca del centro de seguridad de Azure, vea Hola recursos siguientes:

* [Guía de operaciones de planificación de Azure Security Center e](security-center-planning-and-operations-guide.md) : más información cómo tooplan y entender las consideraciones de diseño de hello tooadopt Azure Security Center.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.


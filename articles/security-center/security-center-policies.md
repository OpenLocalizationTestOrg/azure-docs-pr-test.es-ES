---
title: las directivas de seguridad de aaaSet en el centro de seguridad de Azure | Documentos de Microsoft
description: Este documento le ayuda a las directivas de seguridad de tooconfigure en el centro de seguridad de Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Establecimiento de directivas de seguridad en Azure Security Center
Este documento le ayuda a las directivas de seguridad de tooconfigure en el centro de seguridad le guía a través de hello pasos necesarios tooperform esta tarea.

>[!NOTE] 
>A partir de los principios de junio de 2017, centro de seguridad utiliza Hola Microsoft Monitoring Agent toocollect y almacén de los datos. Vea [migración de la plataforma de Azure Security Center](security-center-platform-migration.md) toolearn más. información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>¿Qué son las directivas de seguridad?
Una directiva de seguridad define el conjunto de Hola de controles, que se recomiendan para los recursos dentro de hello especificado suscripción. En el centro de seguridad, definir directivas para las suscripciones de Azure según las necesidades de seguridad de empresa tooyour y tipo de Hola de aplicaciones o confidencialidad de datos de hello en cada suscripción.

Por ejemplo, es posible que los recursos usados para el desarrollo o las pruebas tengan requisitos de seguridad diferentes a los de los recursos que se emplean para aplicaciones de producción. Del mismo modo, es posible que las aplicaciones que usan datos regulados, como la información de identificación personal, requieran un mayor nivel de seguridad. Directivas de seguridad que se permiten en las recomendaciones de seguridad de unidad de Azure Security Center y supervisión toohelp posibles vulnerabilidades de identificar y mitigar las amenazas. Lectura [planeación de centro de seguridad de Azure y la Guía de operaciones de](security-center-planning-and-operations-guide.md) para obtener más información acerca de cómo toodetermine Hola opción que es adecuada para usted.

## <a name="set-security-policies"></a>Configuración de directivas de seguridad
Puede configurar directivas de seguridad para cada suscripción. toomodify una directiva de seguridad, debe ser propietario o colaborador de esa suscripción. Inicie sesión en toohello portal de Azure y siga Hola que sigue los pasos en el centro de seguridad de las directivas de seguridad tooconfigure:

1. Haga clic en hello **directiva** el icono Panel de centro de seguridad de Hola.
2. En la hoja de la directiva de seguridad Hola que se abre, seleccione suscripción Hola que servirá de directiva de seguridad de tooenable Hola.

    ![Definición de directiva](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Hola **directiva de seguridad** hoja para la suscripción de hello seleccionado se abre con un conjunto de opciones. Hola opciones disponibles en esta hoja son:

   * **Directivas de prevención**: Utilice esta directivas de tooconfigure opción por suscripción.  
   * **Notificación por correo electrónico**: Utilice esta tooconfigure opción una notificación de correo electrónico que se envía en hello primera diaria aparición de una alerta y las alertas de gravedad alta. Las preferencias de correo electrónico solo pueden configurarse para las directivas de suscripción. Lectura [proporcionar detalles de contacto de seguridad en Azure Security Center](security-center-provide-security-contact-details.md) para obtener más información acerca de cómo tooconfigure una notificación por correo electrónico.
   * **Nivel de precios**: Utilice esta Hola de tooupgrade opción selección de nivel de precios. Vea [precios del centro de seguridad](security-center-pricing.md) toolearn más sobre los precios de opciones.
4. Asegúrese de que la opción **Recopilar datos de máquinas virtuales** está **Activada**. Esta opción habilita la recopilación de inicio de sesión automático para los recursos nuevos y existentes mediante Hola Microsoft Monitoring Agent: se trata de hello mismo agente utilizado por servicio de Operations Management Suite y análisis de registros de Hola. Los datos recopilados de este agente se almacenan en un espacios de trabajo de análisis de registros existente asociada a su suscripción de Azure o áreas de trabajo nuevo, teniendo en geografía de Hola de cuenta de hello máquina virtual.

5. Hola **directiva de seguridad** hoja, haga clic en **directivas de prevención** toosee Hola opciones disponibles. Haga clic en **en** recomendaciones de seguridad de hello tooenable que son relevantes para esta suscripción.

    ![Al seleccionar las directivas de seguridad de Hola](./media/security-center-policies/security-center-policies-fig7.png)

Usar cada opción de Hola como un toounderstand de referencia en la tabla siguiente:

| Directiva | Cuando el estado es Activado |
| --- | --- |
| Actualizaciones del sistema |Recupera una lista diaria de las actualizaciones críticas y de seguridad disponibles en Windows Update o Windows Server Update Services. Hola ha recuperado la lista depende de servicio de Hola que está configurado para que la máquina virtual y recomienda que se aplican las actualizaciones que faltan de Hola. Para los sistemas Linux, directiva de hello usa Hola paquetes de distribución administración sistema toodetermine paquetes que tienen actualizaciones disponibles. También comprueba las actualizaciones de seguridad y críticas de las máquinas virtuales de [Azure Cloud Services](../cloud-services/cloud-services-how-to-configure.md). |
| Vulnerabilidades del SO |Analiza configuraciones diaria toodetermine problemas del sistema operativo que pudieron realizar tooattack vulnerables de hello máquina virtual. Directiva de Hello también recomienda tooaddress de cambios de configuración estas vulnerabilidades. Vea hello [lista de líneas de base recomendadas](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) para obtener más información sobre configuraciones específicas de Hola que se está supervisando. (En este momento, Windows Server 2016 no es totalmente compatible). |
| Endpoint Protection |Recomienda endpoint protection toobe aprovisionado para todas las máquinas virtuales de Windows toohelp identificar y quitar virus, spyware y otro software malintencionado. |
| Cifrado de discos |Le recomienda habilitar el cifrado de disco todas las máquinas virtuales tooenhance protección de datos en reposo. |
| Grupos de seguridad de red |Recomienda que [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) ser configurado toocontrol entrantes y salientes tráfico tooVMs que tienen extremos públicos. Todas las interfaces de red de máquina virtual heredan los grupos de seguridad de red configurados para una subred, a menos que se especifique lo contrario. Además toochecking que se ha configurado un grupo de seguridad de red, esta directiva evalúa reglas de tooidentify de reglas de seguridad de entrada que permiten el tráfico entrante. |
| Firewall de aplicaciones web |Recomienda que un servidor de seguridad de la aplicación web se aprovisionen en máquinas virtuales cuando se cumple cualquiera de los siguientes hello: </br></br>[Dirección IP pública de nivel de instancia](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) se usa y reglas de seguridad de entrada para el grupo de seguridad de red asociado Hola Hola son tooallow configurado acceso tooport 80/443.</br></br>Se utiliza con equilibrio de carga IP y Hola asociados de equilibrio de carga y reglas de NAT (traducción) de direcciones de red de entrada son tooallow configurado acceso tooport 80/443. Para más información, consulte [Compatibilidad de Azure Resource Manager con Load Balancer](../load-balancer/load-balancer-arm.md). |
| Firewall de próxima generación |Amplía las medidas de protección de la red más allá de los grupos de seguridad de red, que están integrados en Azure. Centro de seguridad detectará las implementaciones para el que un firewall de generación siguiente, se recomienda y habilitar tooprovision un dispositivo virtual. |
| Auditoría de SQL y detección de amenazas |Recomienda que se la auditoría de acceso tooAzure base de datos habilitada para el cumplimiento de normas y también avanzada la detección de amenazas, por razones de investigación. |
| Cifrado de SQL |Recomienda que el cifrado en reposo se habilite para Azure SQL Database, las copias de seguridad asociadas y los archivos de registro de transacciones. De esta forma, aunque haya infracción de datos, no se podrán leer. |
| Evaluación de vulnerabilidades |Se recomienda instalar una solución de evaluación de vulnerabilidades en la máquina virtual. |
| Cifrado de almacenamiento |Actualmente, esta característica está disponible para los archivos y blobs de Azure. Después de habilitar Cifrado del servicio Storage, solo se cifrarán los datos nuevos, mientras que los archivos existentes en esta cuenta de almacenamiento permanecerán sin cifrar. |
| Acceso de red JIT |Cuando se habilita justo a tiempo, el centro de seguridad para bloquear el tráfico entrante tooyour máquinas virtuales de Azure mediante la creación de una regla de NSG. Seleccionar puertos hello en hello VM toowhich debe bloquear el tráfico entrante. Para más información, consulte [Administrar el acceso a máquina virtual mediante Just-In-Time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time). |

Después de configurar todas las opciones, haga clic en **Aceptar** en hello **directiva de seguridad** hoja que contiene recomendaciones de hello y, a continuación, haga clic en **guardar** en hello **seguridad Directiva** hoja que tenga una configuración inicial Hola.

> [!NOTE]
> Hola tarifa sigue siendo aplicable para el nivel de grupo de recursos de Hola. Para obtener más información visite hello [precios](https://azure.microsoft.com/pricing/details/security-center/) página.
>
>

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo tooconfigure las directivas de seguridad en el centro de seguridad de Azure. toolearn más información acerca del centro de seguridad de Azure, vea Hola recursos siguientes:

* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md). Obtenga información acerca de cómo tooplan y entender las consideraciones de diseño de hello tooadopt Azure Security Center.
* [Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md). Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md). Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md). Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md). Busque las preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/). Encuentre artículos de blog sobre el cumplimiento y la seguridad de Azure.

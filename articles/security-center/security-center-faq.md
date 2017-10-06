---
title: "Centro de seguridad de preguntas más frecuentes (P+F) aaaAzure | Documentos de Microsoft"
description: "Estas preguntas más frecuentes responden a las preguntas sobre el Centro de seguridad de Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Preguntas más frecuentes sobre el Centro de seguridad de Azure
Estas preguntas más frecuentes responden a preguntas acerca del centro de seguridad de Azure, un servicio que le ayuda a evitar, detectar y responder toothreats con una mayor visibilidad y control sobre la seguridad de Hola de los recursos de Microsoft Azure.

> [!NOTE]
> A partir de los principios de junio de 2017, centro de seguridad usará Hola Microsoft Monitoring Agent toocollect y almacenar datos. más información, consulte toolearn [migración de la plataforma de Azure Security Center](security-center-platform-migration.md). información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>
>

## <a name="general-questions"></a>Preguntas generales
### <a name="what-is-azure-security-center"></a>¿Qué es el Centro de seguridad de Azure?
Centro de seguridad de Azure le ayuda a evitar, detectar y responder toothreats con una mayor visibilidad y control sobre la seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

### <a name="how-do-i-get-azure-security-center"></a>¿Cómo puedo obtener el Centro de seguridad de Azure?
Centro de seguridad de Azure está habilitada con su suscripción de Microsoft Azure y accesibles desde hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/). ([Iniciar sesión en el portal de toohello](https://portal.azure.com), seleccione **examinar**y se desplaza demasiado**centro de seguridad**).  

## <a name="billing"></a>Facturación
### <a name="how-does-billing-work-for-azure-security-center"></a>¿Cómo funciona la facturación para el Centro de seguridad de Azure?
Security Center se ofrece en dos niveles:

Hola **nivel gratuito** proporciona visibilidad en estado de seguridad de Hola de los recursos de Azure, la directiva de seguridad básica, las recomendaciones de seguridad e integración con servicios y productos de seguridad de los socios.

Hola **nivel estándar** agrega avanzada amenaza las capacidades de detección, incluidos intelligence, análisis del comportamiento, detección de anomalías, incidentes de seguridad de amenazas e informes de atribución de amenaza. nivel estándar de Hello es gratuita para hello primeros 60 días. Si decide que el servicio de hello toocontinue toouse más allá de 60 días, se iniciará automáticamente toocharge para servicio de Hola.  tooupgrade, seleccione nivel de precios en hello [directiva de seguridad](security-center-policies.md#set-security-policies). más información, consulte toolearn [precios del centro de seguridad](security-center-pricing.md).

## <a name="permissions"></a>Permisos
Centro de seguridad de Azure usa [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md), lo que proporciona [roles integrados](../active-directory/role-based-access-built-in-roles.md) que se puede asignar toousers, grupos y servicios de Azure.

Centro de seguridad evalúa la configuración de Hola de los problemas de seguridad de recursos tooidentify y vulnerabilidades. En el centro de seguridad, sólo verá información relacionada con recursos tooa cuando se le asigna Hola rol de propietario, Colaborador o lector de hello suscripción o grupo de recursos que pertenece el recurso.

Vea [permisos en el centro de seguridad de Azure](security-center-permissions.md) toolearn más información acerca de los roles y las acciones permitidas en el centro de seguridad.

## <a name="data-collection"></a>Colección de datos
Centro de seguridad recopila datos de sus máquinas virtuales tooassess su estado de seguridad, proporcionar recomendaciones de seguridad y alerta toothreats. La primera vez que se accede al Centro de seguridad la recopilación de datos se habilita en todas las máquinas virtuales de la suscripción. También puede habilitar la recopilación de datos en hello directiva de centro de seguridad.

### <a name="how-do-i-disable-data-collection"></a>¿Cómo se puede deshabilitar la recolección de datos?
Si utiliza capa de centro de seguridad de Azure gratuita de hello, puede deshabilitar la recopilación de datos de máquinas virtuales en cualquier momento. Recopilación de datos es necesaria para las suscripciones en el nivel estándar Hola. Puede deshabilitar la recopilación de datos para una suscripción en hello directiva de seguridad. ([Iniciar sesión en el portal de Azure toohello](https://portal.azure.com), seleccione **examinar**, seleccione **centro de seguridad**y seleccione **directiva**.)  Cuando se selecciona una suscripción, una nueva hoja se abre y proporciona Hola tooturn opción desactivada **la recopilación de datos**.

### <a name="how-do-i-enable-data-collection"></a>¿Cómo se puede habilitar la recolección de datos?
Puede habilitar la recopilación de datos para la suscripción de Azure en hello directiva de seguridad. recopilación de datos de tooenable. [Inicie sesión en el portal de Azure toohello](https://portal.azure.com), seleccione **examinar**, seleccione **centro de seguridad**y seleccione **directiva**. Establecer **la recopilación de datos** demasiado**en**.

### <a name="what-happens-when-data-collection-is-enabled"></a>¿Qué sucede cuando se habilita la colección de datos?
Cuando se habilita la recopilación de datos, Hola Microsoft Monitoring Agent se aprovisiona automáticamente en todas las existentes y cualquier admitido nuevas máquinas virtuales que se implementan en la suscripción de Hola.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>¿Es Hola Monitoring Agent influir hello en el rendimiento de Mis servidores?
agente de Hello consume una cantidad nominal de recursos del sistema y debe tener poco impacto en el rendimiento de Hola. Para obtener más información sobre el impacto en el rendimiento y el agente de Hola y la extensión, vea hello [Guía de planeación y las operaciones de](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>¿Dónde se almacenan los datos?
Los datos que recopila este agente se almacenan en un área de trabajo de Log Analytics asociada con la suscripción o en una nueva área de trabajo. Para obtener más información, consulte [Seguridad de datos de Azure Security Center](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Uso del Centro de seguridad de Azure
### <a name="what-is-a-security-policy"></a>¿Qué es una directiva de seguridad?
Una directiva de seguridad define el conjunto de Hola de controles que se recomiendan para los recursos dentro de hello especificado suscripción. En el centro de seguridad de Azure, definir directivas para las suscripciones de Azure según la compañía tooyour requisitos de seguridad y tipo de Hola de aplicaciones o importancia de los datos de hello en cada suscripción.

directivas de seguridad de Hello habilitadas en las recomendaciones de seguridad de unidad de Azure Security Center y la supervisión. toolearn más información acerca de las directivas de seguridad, consulte [supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>¿Quién puede modificar una directiva de seguridad?
toomodify una directiva de seguridad, debe ser un administrador de seguridad o un propietario o colaborador de esa suscripción.

toolearn tooconfigure una directiva de seguridad, vea [establecer directivas de seguridad en Azure Security Center](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>¿Qué es una recomendación de seguridad?
Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure. Las recomendaciones se crean una vez que se identifican las posibles vulnerabilidades de seguridad. Guía de recomendaciones de Hello en proceso de Hola de configuración Hola precisó de control. Algunos ejemplos son:

* Aprovisionamiento de antimalware toohelp identificar y quitar software malintencionado
* Configuración de [grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) y máquinas de toocontrol tráfico toovirtual de reglas
* Aprovisionamiento de un toohelp de firewall de aplicación web defenderse contra los ataques que se dirige a las aplicaciones web
* Implementación de actualizaciones del sistema que faltan.
* Direccionamiento de las configuraciones de sistema operativo que no coincide con hello recomienda líneas de base

Aquí solo se muestran las recomendaciones habilitadas en las directivas de seguridad.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>¿Cómo se puede ver el estado de seguridad actual de Hola de los recursos de Azure?
Hola **información general sobre el centro de seguridad** hoja muestra Hola postura de seguridad general de su entorno desglosado por proceso, redes, almacenamiento y datos y aplicaciones. Cada tipo de recurso tiene un indicador que muestra si se ha identificado alguna posible vulnerabilidad de seguridad. Al hacer clic en cada icono muestra una lista de problemas de seguridad identificado por el centro de seguridad, junto con un inventario de los recursos de hello en su suscripción.

### <a name="what-triggers-a-security-alert"></a>¿Qué desencadena una alerta de seguridad?
Centro de seguridad de Azure automáticamente recopila, analiza y fusibles datos de registro de recursos de Azure, redes de Hola y soluciones de socios como antimalware y firewalls. Cuando se detecten amenazas, se creará una alerta de seguridad. Como ejemplos se incluye la detección de:

* Máquinas virtuales en peligro que se comunican con direcciones IP malintencionadas conocidas.
* Malware avanzado detectado mediante la generación de informes de errores de Windows.
* Ataques por fuerza bruta contra máquinas virtuales.
* Alertas de seguridad de soluciones de seguridad integradas de socio, como antimalware o Firewall de aplicaciones web.

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>¿Cuál es la diferencia de hello entre amenazas detecta y alertas en por Microsoft Security Response Center frente a Azure Security Center?
Hola Microsoft Security Response Center (MSRC) realiza una supervisión de infraestructura y de red de Azure Hola seleccione seguridad y recibe las quejas de inteligencia y controlar el abuso de amenaza de terceros. Cuando se tenga en cuenta que los datos del cliente se ha accedido a una parte ilegal o no autorizado o uso de ese cliente Hola de Azure no cumple con los términos de Hola de uso aceptable MSRC, un administrador de incidentes de seguridad notifica a cliente Hola. Notificación normalmente se produce mediante el envío de una seguridad de correo electrónico toohello los contactos especificados en el centro de seguridad de Azure o hello propietario de la suscripción de Azure si no se especifica un contacto de seguridad.

Centro de seguridad es un servicio de Azure continuamente supervisa el entorno de Azure del cliente de Hola y aplica análisis tooautomatically detectar una amplia variedad de actividades malintencionadas. Estas detecciones se exponen como alertas de seguridad en el panel del centro de seguridad de Hola.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>¿Qué recursos de Azure supervisa Azure Security Center?
Centro de seguridad de Azure supervisa hello Azure recursos siguientes:

* Máquinas virtuales (se incluyen [Cloud Services](../cloud-services/cloud-services-choose-me.md))
* Redes virtuales de Azure
* Servicio de SQL Azure
* Cuenta de almacenamiento de Azure
* Azure Web Apps ([en App Service Environment](../app-service/app-service-app-service-environments-readme.md))
* Soluciones de asociados integradas en su suscripción de Azure, como un firewall de aplicaciones web en las máquinas virtuales y en [App Service Environment](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Virtual Machines
### <a name="what-types-of-virtual-machines-are-supported"></a>¿Qué tipos de máquinas virtuales se admiten?
Supervisión y las recomendaciones están disponibles para las máquinas virtuales (VM) creadas con ambos hello [clásico y modelos de implementación del Administrador de recursos](../azure-classic-rm.md).

Consulte [Plataformas compatibles con Azure Security Center](security-center-os-coverage.md) para ver una lista de plataformas compatibles.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>¿Por qué no reconoce Azure Security Center solución antimalware de hello ejecutando en mi máquina virtual de Azure?
Azure Security Center solo tiene visibilidad del antimalware instalado mediante extensiones de Azure. Por ejemplo, el centro de seguridad no es capaz de toodetect antimalware que estaba previamente instalado en una imagen proporcionada o si instaló antimalware en sus máquinas virtuales mediante sus propios procesos (como sistemas de administración de configuración).

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>¿Por qué aparece el mensaje de Hola "Datos de análisis que faltan" para mi máquina virtual?
Este mensaje aparece cuando no hay datos de examen de una máquina virtual. Puede tardar algún tiempo (menos de una hora) para toopopulate de datos de detección una vez habilitada la recopilación de datos en el centro de seguridad de Azure. Una vez rellenado inicial de Hola de datos de análisis, puede recibir este mensaje porque no hay ningún dato de análisis o no hay ningún dato de detección recientes. Estos análisis no se rellenan para las máquinas virtuales que estén detenidas. Este mensaje también podría aparecer si no se rellenan de datos de análisis recientemente (de acuerdo con directiva de retención de hello para el agente de Windows hello, que tiene un valor predeterminado de 30 días).

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>¿Por qué aparece un mensaje de bienvenida que "Agente de máquina virtual está ausente?"
Hola agente de máquina virtual debe estar instalado en las máquinas virtuales tooenable la recopilación de datos. Hola agente de máquina virtual está instalado de forma predeterminada para las máquinas virtuales que se implementan desde hello Azure Marketplace. Para obtener información sobre cómo tooinstall Hola agente de máquina virtual en otras máquinas virtuales, consulte el blog de hello [agente de máquina virtual y extensiones](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).

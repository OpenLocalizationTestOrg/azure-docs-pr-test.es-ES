---
title: "aaaAzure centro de seguridad y máquinas virtuales de Azure | Documentos de Microsoft"
description: "Este documento le ayuda toounderstand cómo Azure Security Center puede protegerle máquinas virtuales de Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Azure Security Center y Azure Virtual Machines
[Centro de seguridad de Azure](https://azure.microsoft.com/services/security-center/) le ayuda a evitar, detectar y responder toothreats. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

En este artículo se explica cómo Security Center puede ayudarle a proteger las instancias de Azure Virtual Machines (VM).

## <a name="why-use-security-center"></a>Razones para usar Security Center
Security Center le ayuda a proteger los datos de máquinas virtuales en Azure proporcionando visibilidad en la configuración de seguridad de su máquina virtual. Cuando el centro de seguridad protege las máquinas virtuales, Hola después capacidades estarán disponible:

* Configuración de seguridad del sistema operativo (SO) con hello recomienda las reglas de configuración
* Seguridad del sistema y actualizaciones críticas que faltan
* Recomendaciones de protección de puntos de conexión
* Validación de cifrado de disco
* Evaluación y corrección de vulnerabilidades
* Detección de amenazas

Además toohelping proteger las máquinas virtuales de Azure, el centro de seguridad también proporciona supervisión de la seguridad y la administración de servicios en la nube, servicios de aplicaciones, redes virtuales y mucho más. 

> [!NOTE]
> Vea [Introducción tooAzure centro de seguridad](security-center-intro.md) toolearn más acerca del centro de seguridad de Azure.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
tooget a trabajar con el centro de seguridad de Azure, podrá necesita tooknow y tenga en cuenta Hola siguiente:

* Debe tener un tooMicrosoft de suscripción a Azure. Para más información sobre los niveles Gratis y Estándar de Security Center, consulte [Precios de Security Center](https://azure.microsoft.com/pricing/details/security-center/).
* Planear la adopción de centro de seguridad, consulte [Guía de planeación y las operaciones de Azure Security Center](security-center-planning-and-operations-guide.md) toolearn más acerca de las consideraciones de planeación y las operaciones.
* Para más información sobre la compatibilidad del sistema operativo, consulte [Preguntas más frecuentes (P+F) sobre Azure Security Center](security-center-faq.md). 

## <a name="set-security-policy"></a>Establecimiento de directivas de seguridad
Toobe de necesidades de recopilación de datos habilitado de modo que ese centro de seguridad de Azure puede recopilar información de hello necesita tooprovide recomendaciones y las alertas generadas se basa en la directiva de seguridad de Hola que configure. En la siguiente ilustración de hello, puede ver que **la recopilación de datos** se ha activado **en**.

Una directiva de seguridad define el conjunto de Hola de controles que se recomiendan para los recursos dentro de hello especificado suscripción o grupo de recursos. Antes de habilitar la directiva de seguridad, debe tener habilitada la recopilación de datos, el centro de seguridad recopila datos de las máquinas virtuales en orden tooassess su estado de seguridad, se proporcionan recomendaciones de seguridad y avisarle toothreats. En el centro de seguridad, definir directivas para sus suscripciones de Azure o grupos de recursos según tooyour las necesidades de seguridad y empresa tipo hello de aplicaciones o importancia de los datos de hello en cada suscripción. 

![Directiva de seguridad](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> toolearn más información acerca de cada uno de ellos **directivas de prevención** disponible, vea [establecer directivas de seguridad](security-center-policies.md) artículo.
> 
> 

## <a name="manage-security-recommendations"></a>Administración de recomendaciones de seguridad
Centro de seguridad analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el Centro de seguridad identifica vulnerabilidades de seguridad potenciales, crea recomendaciones. recomendaciones de Hello guiarle por proceso de Hola de configuración de controles de Hola que sea necesitado.

Después de establecer una directiva de seguridad, el centro de seguridad analiza el estado de seguridad de Hola de sus tooidentify posibles vulnerabilidades de recursos. recomendaciones de Hola se muestran en un formato de tabla, donde cada línea representa una recomendación concreta. tabla de Hello siguiente proporciona algunos ejemplos de las recomendaciones para máquinas virtuales de Azure y cada uno de ellos lo que sucederá si se aplica. Cuando se selecciona una recomendación, se proporcionará información que muestra cómo tooimplement Hola recomendación en el centro de seguridad.

| Recomendación | Description |
| --- | --- |
| [Habilitar la colección de datos de las suscripciones](security-center-enable-data-collection.md) |Se recomienda activar la recopilación de datos en la directiva de seguridad de Hola para cada una de las suscripciones y todas las máquinas virtuales (VM) en el nodo suscripciones. |
| [Corrección de vulnerabilidades del SO](security-center-remediate-os-vulnerabilities.md) |P. ej., recomienda alinear las configuraciones de sistema operativo con hello las reglas de configuración, se recomienda no permiten toobe contraseñas guardado. |
| [Aplicar actualizaciones del sistema](security-center-apply-system-updates.md) |Se recomienda que implemente tooVMs actualizaciones críticas y seguridad del sistema que faltan. |
| [Reiniciar tras actualizar el sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomienda que reinicie un proceso de máquina virtual toocomplete Hola de aplicar las actualizaciones del sistema. |
| [Instalación de Endpoint Protection](security-center-install-endpoint-protection.md) |Recomienda que aprovisione tooVMs de programas antimalware (sólo VM de Windows). |
| [Resolver alertas de estado de Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomienda resolver los errores de Endpoint Protection. |
| [Habilitar el Agente de máquina virtual](security-center-enable-vm-agent.md) |Permite toosee que las máquinas virtuales requieren Hola a agente de máquina virtual. Hola agente de máquina virtual debe instalarse en máquinas virtuales en la detección, análisis de la línea de base y los programas antimalware de revisiones de tooprovision de orden. Hola agente de máquina virtual está instalado de forma predeterminada para las máquinas virtuales que se implementan desde hello Azure Marketplace. artículo de Hello [agente de máquina virtual y extensiones: parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) proporciona información acerca de cómo tooinstall Hola agente de máquina virtual. |
| [Aplicar cifrado de discos](security-center-apply-disk-encryption.md) |Se recomienda cifrar los discos de la máquina virtual mediante Cifrado de discos de Azure (máquinas virtuales Linux y Windows). El cifrado se recomienda para hello SO y volúmenes de datos en la máquina virtual. |
| [Evaluación de vulnerabilidades no instalada](security-center-vulnerability-assessment-recommendations.md) |Se recomienda instalar una solución de evaluación de vulnerabilidades en la máquina virtual. |
| [Corrección de vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Le permite toosee vulnerabilidades de sistema y las aplicaciones detectadas por la solución de evaluación de vulnerabilidades de hello instalado en la máquina virtual. |

> [!NOTE]
> toolearn más información acerca de las recomendaciones, consulte [administrar las recomendaciones de seguridad](security-center-recommendations.md) artículo.
> 
> 

## <a name="monitor-security-health"></a>Supervisión del estado de la seguridad
Después de habilitar [las directivas de seguridad](security-center-policies.md) para obtener recursos de una suscripción, el centro de seguridad analizará seguridad Hola de sus tooidentify posibles vulnerabilidades de recursos.  Puede ver Hola de estado de seguridad de los recursos, junto con cualquier problema en hello **estado de seguridad del recurso** hoja. Al hacer clic en **máquinas virtuales** en hello **seguridad de los recursos** el icono de estado, hello **máquinas virtuales** hoja se abrirá con las recomendaciones para las máquinas virtuales. 

![Estado de la seguridad](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Administrar y responder a alertas de toosecurity
Centro de seguridad automáticamente recopila, analiza y se integra datos de registro de recursos de Azure, redes de Hola y soluciones de socios conectados (como punto de conexión y de firewall de soluciones de protección), toodetect reales amenazas y reducir los falsos positivos. Mediante el aprovechamiento de una agregación de diversos [las capacidades de detección](security-center-detection-capabilities.md), centro de seguridad es capaz de toogenerate un nivel de prioridad seguridad alertas toohelp investigar el problema de Hola y proporcionar recomendaciones sobre cómo rápidamente tooremediate posibles ataques.

![Alertas de seguridad](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Seleccione un toolearn de alerta de seguridad más información acerca de los eventos de Hola que desencadenó la alerta de Hola y qué, si existe, los pasos necesitan tootake tooremediate un ataque. Las alertas de seguridad se agrupan según el [tipo](security-center-alerts-type.md) y la fecha.

## <a name="see-also"></a>Otras referencias
toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.


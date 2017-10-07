---
title: vulnerabilidades de aaaRemediate sistema operativo en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** SO corregir vulnerabilidades **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Corrección de vulnerabilidades del SO en Azure Security Center
Centro de seguridad de Azure diariamente analiza el sistema de operativo (SO) de máquina virtual (VM) para las configuraciones que pudieron realizar Hola VM cambios de configuración sean más vulnerable de tooattack y recomienda tooaddress estas vulnerabilidades. Centro de seguridad, se recomienda que resolver vulnerabilidades cuando la configuración del sistema operativo de la máquina virtual no coincide con hello reglas de configuración recomendada.

> [!NOTE]
> Para obtener más información sobre configuraciones específicas de Hola que se está supervisando, vea hello [lista de reglas de configuración recomendada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  Este documento no es una guía paso a paso.
>
>

1. Hola **recomendaciones** hoja, seleccione **vulnerabilidades de sistema operativo corregir**.
   ![Corrección de vulnerabilidades del SO][1]

    Hola **vulnerabilidades de sistema operativo corregir** hoja se abre y muestra las máquinas virtuales con las configuraciones de sistema operativo que no coincide con hello reglas de configuración recomendada.  Para cada máquina virtual, hoja de hello identifica:

   * **No se pudo reglas** --hello número de reglas que Hola configuración del sistema operativo de la máquina virtual con error.
   * **HORA del último RECORRIDO** : fecha de Hola y tiempo que el centro de seguridad última vez la configuración del sistema operativo de la máquina virtual de Hola.
   * **ESTADO** : Hola estado actual de vulnerabilidades de hello:

     * Abierta: vulnerabilidades de hello no se ha solucionado aún
     * En curso: Una vulnerabilidad de saludo se está aplicando actualmente, no se requiere ninguna acción por parte del usuario
     * Resolver: vulnerabilidades de hello ya se ha solucionado (cuando se ha resuelto el problema de hello, entrada Hola está atenuado)
   * **GRAVEDAD** --todas las vulnerabilidades se establecen tooa gravedad baja, lo que significa que debe llevar a cabo una vulnerabilidad, pero no requiere atención inmediata.

2. Seleccione una máquina virtual. Una hoja para VM se abre y muestra las reglas de Hola que han producido un error.
   ![Reglas de configuración con error][2]

3. Seleccione una regla. En este ejemplo, seleccionamos **La contraseña debe cumplir los requisitos de complejidad**. Una hoja abre el impacto de hello y regla de hello no se pudo que describe. Revise los detalles de Hola y tenga en cuenta cómo se aplican las configuraciones del sistema operativo.
  ![Descripción de la regla de error de Hola][3]

  Centro de seguridad utiliza identificadores únicos de tooassign Common Configuration Enumeration (CCE) para las reglas de configuración. Hola siguiente información se proporciona en esta hoja:

  - NOMBRE: nombre de la regla.
  - GRAVEDAD: valor de gravedad de CCE, que puede ser Crítico, Importante o Advertencia.
  - CCIED--Identificador único CCE para regla de Hola
  - DESCRIPCIÓN: descripción de la regla.
  - VULNERABILIDAD: explicación de la vulnerabilidad o el riesgo si no se aplica la regla.
  - IMPACTO: impacto de negocio cuando se aplica la regla.
  - VALOR esperado: Valor que se esperaba al centro de seguridad analiza la configuración de sistema operativo de la máquina virtual con la regla de Hola
  - OPERACIÓN de regla: Operación utilizada por el centro de seguridad durante el análisis de la configuración del sistema operativo de la máquina virtual con la regla de Hola de reglas
  - VALOR real: Valor devuelto después del análisis de la configuración del sistema operativo de la máquina virtual con la regla de Hola
  - RESULTADO DE LA EVALUACIÓN: resultado del análisis, que puede ser Sin errores o Con errores.

## <a name="see-also"></a>Otras referencias
En este artículo se ha explicado cómo tooimplement Hola centro de seguridad recomendación "corregir SO vulnerabilidades." Puede revisar el conjunto de Hola de reglas de configuración de [aquí](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Centro de seguridad utiliza identificadores únicos de tooassign CCE (enumeración de configuración común) para las reglas de configuración. Visite hello [CCE](https://nvd.nist.gov/cce/index.cfm) sitio para obtener más información.

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Plataformas compatibles con Azure Security Center](security-center-os-coverage.md): proporciona una lista de máquinas virtuales Windows y Linux compatibles.
* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) -Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) -Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) -Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) -Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) -buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png

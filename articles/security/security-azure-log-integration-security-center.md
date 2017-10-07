---
title: "integración de registro con el centro de seguridad aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo trabajar con la integración de registro de alertas del centro de tooget seguridad de Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Cómo tooget el centro de seguridad de las alertas en la integración de registros de Azure
Este artículo proporciona Hola pasos tooenable necesario Hola integración de Azure registro servicio toopull información sobre la alerta de seguridad generado por el centro de seguridad de Azure. Deben haber completado correctamente los pasos de Hola Hola [Introducción](security-azure-log-integration-get-started.md) artículo antes de realizar los pasos de hello en este artículo.

## <a name="detailed-steps"></a>Pasos detallados
Hello siguientes pasos creará Hola necesario entidades de servicio de Azure Active Directory y asignar Hola principio de servicio los toohello suscripción de permisos de lectura:
1. Abra símbolo del sistema de Hola y navegue demasiado**c:\Program Files\Microsoft Azure registro integración**
2. Ejecute el comando de Hola``azlog createazureid``

    Este comando solicita el inicio de sesión de Azure. comando de Hello, a continuación, crea un [entidades de servicio de Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) Hola inquilinos de Azure AD que hospedan Hola suscripciones de Azure en qué Hola usuario registrado es un administrador, un administrador o un propietario. se producirá un error en el comando Hello si Hola usuario registrado es solo un usuario invitado en hello inquilino de Azure AD. TooAzure de autenticación se realiza a través de Azure Active Directory (AD). Crear a una entidad de servicio para la integración de Azlog crea Hola identidad de Azure AD que se concederá acceso tooread de las suscripciones de Azure.

2. A continuación se ejecutará un comando que asigna acceso de lectura en la entidad de servicio toohello Hola suscripción creada en el paso 2. Si no se especifica un Id. de suscripción, comandos de hello intentará tooassign Hola servicio lector principal función tooall suscripciones toowhich tener acceso. </br></br>
``azlog authorize <SubscriptionID>`` </br> por ejemplo: </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Puede ver las advertencias si ejecuta Hola autorizar comando inmediatamente después de comando de createazureid Hola. Hay alguna latencia entre cuando se crea la cuenta de hello Azure AD y cuando la cuenta de hello está disponible para su uso. Si espere aproximadamente 60 segundos después de ejecutar el comando toorun hello de hello createazureid autorizar el comando, no debería ver estas advertencias.

4. Comprobar existen Hola después tooconfirm de carpetas que Hola archivos JSON de registro de auditoría:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Hola de comprobación siguientes tooconfirm de carpetas que existen las alertas del centro de seguridad de ellos:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Si surge algún problema durante la instalación de Hola y configuración, abra una [solicitud de soporte técnico](/azure-supportability/how-to-create-azure-support-request.md), seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la integración de registro de Azure, vea Hola siguientes documentos:

* [Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) (Integración de registros de Microsoft Azure para registros de Azure): Centro de descarga para obtener información, los requisitos del sistema y las instrucciones de instalación de la integración de registros de Azure.
* [Integración de registro de introducción tooAzure](security-azure-log-integration-overview.md) : este documento presenta la integración de registro tooAzure, sus capacidades claves y su funcionamiento.
* [Pasos de configuración de socios comerciales](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) : esta entrada de blog muestra cómo tooconfigure Azure registro toowork integración con soluciones de socios Splunk y ArcSight de HP, IBM QRadar.
* [Preguntas más frecuentes sobre la integración de registro de Azure (P+F)](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre la integración de registro de Azure.
* [Integración de centro de seguridad de integración de registro de alertas con Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) : este documento muestra cómo las alertas toosync centro de seguridad, junto con los eventos de seguridad de máquina virtual recopilados por diagnósticos de Azure y los registros de auditoría de Azure, con los análisis de registros o Solución SIEM.
* [Nuevas características de diagnóstico de Azure y los registros de auditoría de Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : esta entrada de blog presenta tooAzure los registros de auditoría y otras características que le ayudarán a obtienen información sobre las operaciones de Hola de los recursos de Azure.
